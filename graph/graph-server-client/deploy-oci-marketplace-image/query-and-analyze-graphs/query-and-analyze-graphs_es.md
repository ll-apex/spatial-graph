# Consulta y análisis del gráfico

## Introducción

En este ejemplo, se muestra cómo la integración de varios conjuntos de datos y el uso de un gráfico facilitan el análisis adicional y pueden generar nuevas estadísticas. Utilizaremos tres conjuntos de datos pequeños con fines ilustrativos. La primera contiene cuentas y propietarios de cuentas. La segunda es la compra por parte de las personas que poseen esas cuentas. El tercero son las transacciones entre estas cuentas.

El conjunto de datos combinado se utiliza para realizar las siguientes consultas y análisis de gráficos comunes: coincidencia de patrones, detección de ciclos, búsqueda de nodos importantes, detección de comunidades.

El siguiente diagrama de ER muestra las relaciones entre los juegos de datos.

![er-diagrama](images/er-diagram.jpg)

Tiempo de laboratorio estimado: 10 minutos

### Objetivos

*   Aprenda a consultar y analizar el gráfico

### Requisitos

*   El cliente Python activo y en ejecución

## Tarea 1: Obtener el gráfico en la memoria

Suponiendo que el gráfico **customer\_360** ya esté cargado en la memoria en el laboratorio anterior, el gráfico se puede asociar con este comando. Si el gráfico está publicado, también puede acceder al gráfico desde las nuevas sesiones.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

Ahora podemos consultar este gráfico y ejecutar algunos análisis en él.

## Tarea 2: Coincidencia de Patrones

La consulta PGQL es conveniente para detectar patrones específicos.

Busque las cuentas que tuvieron una transferencia entrante y saliente, de más de 500, el mismo día. La consulta PGQL para esto es:

    <copy>
    graph.query_pgql("""
        SELECT a.account_no
             , a.balance
             , t1.amount AS t1_amount
             , t2.amount AS t2_amount
             , t1.transfer_date
        FROM MATCH (a)<-[t1:transfer]-(a1)
           , MATCH (a)-[t2:transfer]->(a2)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
    """).print()
    </copy>
    
    +---------------------------------------------------------------+
    | account_no  | balance | t1_amount | t2_amount | transfer_date |
    +---------------------------------------------------------------+
    | xxx-yyy-202 | 200.0   | 900.0     | 850.0     | 2018-10-06    |
    +---------------------------------------------------------------+
    

## Tarea 3: Detección de ciclos

A continuación, utilizamos PGQL para encontrar una serie de transferencias que comienzan y terminan en la misma cuenta, como de A a B a A, o de A a B a C a A.

La primera consulta se podría expresar como:

    <copy>
    graph.query_pgql("""
        SELECT a1.account_no    AS a1_account
             , t1.transfer_date AS t1_date
             , t1.amount        AS t1_amount
             , a2.account_no    AS a2_account
             , t2.transfer_date AS t2_date
             , t2.amount        AS t2_amount
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
    """).print()
    </copy>
    
    +-----------------------------------------------------------------------------+
    | a1_account  | t1_date    | t1_amount | a2_account  | t2_date    | t2_amount |
    +-----------------------------------------------------------------------------+
    | xxx-yyy-201 | 2018-10-05 | 200.0     | xxx-yyy-202 | 2018-10-10 | 300.0     |
    +-----------------------------------------------------------------------------+
    

Este resultado se visualizará en la siguiente sección:

![detección](images/detection.jpg)

La segunda consulta simplemente agrega una transferencia más al patrón (lista) y se puede expresar como:

    <copy>
    graph.query_pgql("""
        SELECT a1.account_no AS a1_account
             , t1.amount     AS t1_amount
             , a2.account_no AS a2_account
             , t2.amount     AS t2_amount
             , a3.account_no AS a3_account
             , t3.amount     AS t3_amount
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
    """).print()
    </copy>
    
    +-----------------------------------------------------------------------------+
    | a1_account  | t1_amount | a2_account  | t2_amount | a3_account  | t3_amount |
    +-----------------------------------------------------------------------------+
    | xxx-yyy-201 | 500.0     | xxx-yyy-203 | 450.0     | xxx-yyy-204 | 400.0     |
    +-----------------------------------------------------------------------------+
    

Este resultado se visualizará en la siguiente sección:

![detection2](images/detection2.jpg)

## Tarea 4: Cuentas influyentes

Vamos a encontrar qué cuentas son influyentes en la red. Hay varios algoritmos para puntuar la importancia y centralidad de los vértices. Utilizaremos el algoritmo PageRank incorporado como ejemplo.

1.  Filtrar clientes del gráfico. (cf. [Expresiones de filtro](https://docs.oracle.com/cd/E56133_01/latest/prog-guides/filter.html))
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'"));
        graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  Ejecute [PageRank Algorithm](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/pagerank.html). PageRank El algoritmo asigna un peso numérico a cada vértice, midiendo su importancia relativa dentro del gráfico.
    
        <copy>
        analyst.pagerank(graph2);
        </copy>
        
        VertexProperty(name: pagerank, type: double, graph: sub-graph_16)
        
3.  Muestre el resultado.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.account_no, a.pagerank
            FROM MATCH (a)
            ORDER BY a.pagerank DESC
        """).print()
        </copy>
        
        +-------------------------------------+
        | a.account_no | a.pagerank           |
        +-------------------------------------+
        | xxx-yyy-201  | 0.18012007557258927  |
        | xxx-yyy-204  | 0.1412461615467829   |
        | xxx-yyy-203  | 0.1365633635065475   |
        | xxx-yyy-202  | 0.12293884324085073  |
        | xxx-zzz-212  | 0.05987452026569676  |
        | xxx-zzz-211  | 0.025000000000000005 |
        +-------------------------------------+
        

## Tarea 5: Detección de comunidad

Vamos a encontrar qué subconjuntos de cuentas forman comunidades. Es decir, hay más transferencias entre cuentas en el mismo subconjunto que entre esas y cuentas en otro subconjunto. Utilizaremos el algoritmo integrado de componentes débilmente conectados / fuertemente conectados.

1.  El primer paso es crear un subgráfico que solo tenga las cuentas y las transferencias entre ellas. Para ello, cree y aplique un filtro de borde (para bordes con la "transferencia" de lable) al gráfico.
    
    Filtre los clientes del gráfico.
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'")); graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  El algoritmo [Componente débilmente conectado](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/wcc.html) (WCC) detecta solo una partición.
    
        <copy>
        analyst.wcc(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 1)
        
    
    El valor del componente se almacena en una propiedad denominada **wcc**.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.wcc AS component_id
                 , COUNT(*) AS count
            FROM MATCH (a)
            GROUP BY a.wcc
            ORDER BY a.wcc
        """).print()
        </copy>
        
        +----------------------+
        | component_id | count |
        +----------------------+
        | 0            | 6     |
        +----------------------+
        
    
    En este caso, las seis cuentas forman un componente por el algoritmo del CMI.
    
3.  Ejecute un algoritmo [Strongly Connected Component](https://docs.oracle.com/cd/E56133_01/latest/reference//analytics/algorithms/scc.html), SCC Kosaraju. Detecta tres componentes.
    
        <copy>
        analyst.scc_kosaraju(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 3)
        
4.  Muestre los componentes y el número de vértices de cada uno.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.scc_kosaraju AS component_id
                 , COUNT(*) AS count
            FROM MATCH (a)
            GROUP BY a.scc_kosaraju
            ORDER BY a.scc_kosaraju
        """).print()
        </copy>
        
        +----------------------+
        | component_id | count |
        +----------------------+
        | 0            | 1     |
        | 1            | 4     |
        | 2            | 1     |
        +----------------------+
        
5.  Muestre las otras cuentas en el mismo componente conectado que la cuenta de John (= **xxx-yyy-201**). El ID de componente se agrega como una propiedad denominada **SCC\_KOSARAJ** para su uso en consultas PGQL.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.account_no
            FROM MATCH (a)
               , MATCH (a1)
            WHERE a1.account_no = 'xxx-yyy-201'
            AND a.scc_kosaraju = a1.scc_kosaraju
            ORDER BY a.account_no
        """).print()
        </copy>
        
        +-------------+
        | account_no  |
        +-------------+
        | xxx-yyy-201 |
        | xxx-yyy-202 |
        | xxx-yyy-203 |
        | xxx-yyy-204 |
        +-------------+
        
    
    ![comunidad](images/community.jpg)
    
    En este caso, la cuenta **xxx-yyy-201** (cuenta de John), **xxx-yyy-202**, **xxx-yyy-203** y **xxx-yyy-204** forman una partición, la cuenta **xxx-zzz-211** es una parición y la cuenta **xxx-zzz-212** es una partición, mediante el algoritmo SCC Kosaraju.
    

Ahora puede pasar al siguiente laboratorio.

## Reconocimientos

*   **Autor**: Jayant Sharma
*   **Contribuyentes** - Arabella Yao, Jenny Tsai
*   **Última actualización por/fecha**: Ryota Yamanaka, marzo de 2023