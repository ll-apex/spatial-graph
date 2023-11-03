# Crear el gráfico

## Introducción

Ahora, las tablas se crean y rellenan con datos. Vamos a crear una representación gráfica de ellos.

Tiempo estimado: 5 minutos

### Objetivos

Descubra cómo crear un gráfico a partir de orígenes de datos relacionales:

*   Inicio de un cliente (shell de Python) que se conecta al servidor de gráficos
*   Uso del lenguaje de definición de datos (DDL) PGQL (por ejemplo, CREATE PROPERTY GRAPH) para crear una instancia de un gráfico

### Requisitos

*   En esta práctica de laboratorio se asume que ha completado correctamente la práctica de laboratorio: Crear y rellenar tablas.

## Tarea 1: Iniciar el cliente Python

Conéctese a la instancia informática mediante SSH como usuario **opc** mediante la clave privada que ha creado anteriormente.

    <copy>
    ssh -i <private_key> opc@<public_ip_for_compute>
    </copy>
    

Ejemplo:

    <copy>
    ssh -i key.pem opc@203.0.113.14
    </copy>
    

Inicie una instancia de shell de cliente Python que se conecte al servidor.

    <copy>
    opg4py -b https://localhost:7007 -u customer_360
    </copy>
    

Debe ver lo siguiente si el shell de cliente se inicia correctamente.

    <copy>
    password:
    
    Oracle Graph Client Shell 22.4.0
    >>>
    </copy>
    

## Tarea 2: Crear un gráfico

Configure la sentencia create property graph, que crea un gráfico a partir de las tablas existentes.

    <copy>
    statement = '''
    CREATE PROPERTY GRAPH "customer_360"
      VERTEX TABLES (
        customer
      , account
      , merchant
      )
      EDGE TABLES (
        account
          SOURCE KEY(id) REFERENCES account (id)
          DESTINATION KEY(customer_id) REFERENCES customer (id)
          LABEL owned_by PROPERTIES (id)
      , parent_of
          SOURCE KEY(customer_id_parent) REFERENCES customer (id)
          DESTINATION KEY(customer_id_child) REFERENCES customer (id)
      , purchased
          SOURCE KEY(account_id) REFERENCES account (id)
          DESTINATION KEY(merchant_id) REFERENCES merchant (id)
      , transfer
          SOURCE KEY(account_id_from) REFERENCES account (id)
          DESTINATION KEY(account_id_to) REFERENCES account (id)
      ) 
    '''
    </copy>
    

Para obtener más información sobre la sintaxis DDL, consulte [pgql-lang.org](https://pgql-lang.org/spec/1.4/#create-property-graph). Tenga en cuenta que _todas las columnas de las tablas de entrada se asignan a las propiedades de vértices/bordes [por defecto](https://pgql-lang.org/spec/1.4/#properties)_. Para el perímetro **owned\_by**, sólo se proporciona la propiedad **id** con la palabra clave **PROPERTIES** para fines de generación de ID de perímetro, y no se proporcionan las otras propiedades, porque ya están retenidas por los vértices de la cuenta.

Ahora ejecute el DDL de PGQL para crear el gráfico.

    >>> <copy>session.prepare_pgql(statement).execute()</copy>
    False   # This is the expected result
    

## Tarea 3: Comprobar el gráfico recién creado

Compruebe que se ha creado el gráfico. Copie, pegue y ejecute las siguientes sentencias en el shell de Python.

Asocie el gráfico.

    >>> <copy>graph = session.get_graph("customer_360")</copy>
    

Compruebe que se ha creado el gráfico.

    >>> <copy>graph</copy>
    PgxGraph(name: customer_360, v: 15, e: 24, directed: True, memory(Mb): 0)
    

Ejecute algunas consultas PGQL. Por ejemplo, la lista de etiquetas de vértice:

    <copy>
    graph.query_pgql("""
      SELECT DISTINCT LABEL(v) FROM MATCH (v)
    """).print()
    </copy>
    
    +----------+
    | LABEL(v) |
    +----------+
    | ACCOUNT  |
    | CUSTOMER |
    | MERCHANT |
    +----------+
    

Número de vértices con cada etiqueta:

    <copy>
    graph.query_pgql("""
      SELECT COUNT(v), LABEL(v) FROM MATCH (v) GROUP BY LABEL(v)
    """).print()
    </copy>
    
    +---------------------+
    | COUNT(v) | LABEL(v) |
    +---------------------+
    | 5        | MERCHANT |
    | 6        | ACCOUNT  |
    | 4        | CUSTOMER |
    +---------------------+
    

La lista de etiquetas de borde:

    <copy>
    graph.query_pgql("""
      SELECT DISTINCT LABEL(e) FROM MATCH ()-[e]->()
    """).print()
    </copy>
    
    +-----------+
    | LABEL(e)  |
    +-----------+
    | OWNED_BY  |
    | PARENT_OF |
    | PURCHASED |
    | TRANSFER  |
    +-----------+
    

Cuántos bordes con cada etiqueta:

    <copy>
    graph.query_pgql("""
      SELECT COUNT(e), LABEL(e) FROM MATCH ()-[e]->() GROUP BY LABEL(e)
    """).print()
    </copy>
    
    +----------------------+
    | COUNT(e) | LABEL(e)  |
    +----------------------+
    | 4        | OWNED_BY  |
    | 8        | TRANSFER  |
    | 1        | PARENT_OF |
    | 11       | PURCHASED |
    +----------------------+
    

## Tarea 4: Publicar el gráfico

El gráfico recién creado es "privado" por defecto y solo se puede acceder a él desde la sesión actual. Para acceder al gráfico desde nuevas sesiones en el futuro, puede "publicar" el gráfico.

A continuación, vuelva a crear el gráfico siguiendo el procedimiento anterior y publíquelo.

    <copy>
    graph.publish()
    </copy>
    

La próxima vez que se conecte, podrá acceder al gráfico guardado en la memoria sin volver a cargarlo, si el servidor de gráficos no se ha cerrado ni reiniciado entre conexiones.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

Tenga en cuenta que puede publicar gráficos porque se ha otorgado el rol **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** cuando se crea el usuario. De lo contrario, el usuario **ADMIN** debe otorgarlo y volver a conectarse al shell de Python para seleccionar los permisos actualizados.

Ahora puede pasar a la siguiente práctica de laboratorio.

## Reconocimientos

*   **Autor**: Jayant Sharma
*   **Contribuyentes** - Arabella Yao, Jenny Tsai
*   **Última actualización por/fecha**: Ryota Yamanaka, marzo de 2023