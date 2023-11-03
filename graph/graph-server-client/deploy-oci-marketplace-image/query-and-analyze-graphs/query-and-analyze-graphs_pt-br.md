# Consultar e Analisar o Gráfico

## Introdução

Este exemplo mostra como a integração de vários conjuntos de dados e o uso de um gráfico facilitam análises adicionais e podem levar a novos insights. Utilizaremos três pequenos conjuntos de dados para fins ilustrativos. O primeiro contém contas e proprietários de contas. A segunda é a compra das pessoas que possuem essas contas. A terceira é a transação entre essas contas.

O conjunto de dados combinado é então usado para executar as seguintes consultas e análises de gráficos comuns: correspondência de padrões, detecção de ciclos, localização de nós importantes, detecção de comunidade.

O diagrama de ER a seguir ilustra os relacionamentos entre os conjuntos de dados.

![er-diagrama](images/er-diagram.jpg)

Tempo de Laboratório Estimado: 10 minutos

### Objetivos

*   Saiba como consultar e analisar o gráfico

### Pré-requisitos

*   O cliente Python ativo e em execução

## Tarefa 1: Obter o Gráfico na Memória

Supondo que o gráfico **customer\_360** já esteja carregado na memória no Laboratório anterior, o gráfico pode ser anexado a esse comando. Se o gráfico for publicado, você também poderá acessá-lo nas novas sessões.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

Agora podemos consultar este gráfico e executar algumas análises nele.

## Tarefa 2: Correspondência de Padrão

A Consulta PGQL é conveniente para detectar padrões específicos.

Localize contas que tenham uma transferência de entrada e saída, de mais de 500, no mesmo dia. A consulta PGQL para isso é:

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
    

## Tarefa 3: Detecção de Ciclos

Em seguida, usamos o PGQL para encontrar uma série de transferências que começam e terminam na mesma conta, como A a B a A, ou A a B a C a A.

A primeira consulta pode ser expressa como:

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
    

Esse resultado será visualizado na próxima seção:

![detecção](images/detection.jpg)

A segunda consulta apenas adiciona mais uma transferência ao padrão (lista) e pode ser expressa como:

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
    

Esse resultado será visualizado na próxima seção:

![detection2](images/detection2.jpg)

## Tarefa 4: Contas Influentes

Vamos descobrir quais contas são influentes na rede. Existem vários algoritmos para pontuar a importância e a centralidade dos vértices. Usaremos o algoritmo PageRank incorporado como exemplo.

1.  Filtre clientes do gráfico. (cf. [Filtrar Expressões](https://docs.oracle.com/cd/E56133_01/latest/prog-guides/filter.html))
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'"));
        graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  Execute [PageRank Algorithm](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/pagerank.html). PageRank O algoritmo atribui um peso numérico a cada vértice, medindo sua importância relativa dentro do gráfico.
    
        <copy>
        analyst.pagerank(graph2);
        </copy>
        
        VertexProperty(name: pagerank, type: double, graph: sub-graph_16)
        
3.  Mostre o resultado.
    
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
        

## Tarefa 5: Detecção da Comunidade

Vamos descobrir quais subconjuntos de contas formam comunidades. Ou seja, há mais transferências entre contas no mesmo subconjunto do que entre elas e contas em outro subconjunto. Usaremos o algoritmo incorporado de componentes fracamente / fortemente conectados.

1.  O primeiro passo é criar um subgráfico que tenha apenas as contas e as transferências entre elas. Isso é feito criando e aplicando um filtro de borda (para bordas com o lable "transfer") para o gráfico.
    
    Filtre clientes do gráfico.
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'")); graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  O algoritmo [Componente Conectado Inadequadamente](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/wcc.html) (WCC) detecta apenas uma partição.
    
        <copy>
        analyst.wcc(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 1)
        
    
    O valor do componente é armazenado em uma propriedade denominada **wcc**.
    
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
        
    
    Nesse caso, todas as seis contas formam um componente pelo algoritmo WCC.
    
3.  Execute um algoritmo [Componente Fortemente Conectado](https://docs.oracle.com/cd/E56133_01/latest/reference//analytics/algorithms/scc.html), SCC Kosaraju. Detecta três componentes.
    
        <copy>
        analyst.scc_kosaraju(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 3)
        
4.  Liste os componentes e o número de vértices em cada um.
    
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
        
5.  Liste as outras contas no mesmo componente conectado que a conta de John (= **xxx-yyy-201**). O ID do componente é adicionado como uma propriedade chamada **SCC\_KOSARAJ** para uso em consultas PGQL.
    
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
        
    
    ![comunidade](images/community.jpg)
    
    Nesse caso, a conta **xxx-yyy-201** (conta de John), **xxx-yyy-202**, **xxx-yyy-203** e **xxx-yyyy-204** formam uma partição, a conta **xxx-zzz-211** é uma partição e a conta **xxx-zzz-212** é uma partição, pelo algoritmo SCC Kosaraju.
    

Agora você pode prosseguir para o próximo Laboratório.

## Agradecimentos

*   **Autor** - Jayant Sharma
*   **Colaboradores** - Arabella Yao, Jenny Tsai
*   **Última Atualização em/Data** - Ryota Yamanaka, março de 2023