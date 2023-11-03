# Consultas espaciales

## Introducción

Este laboratorio le guiará a través de consultas espaciales básicas en Oracle Autonomous Database. Utilizará los datos de ejemplo creados en el laboratorio anterior para identificar elementos en función de la proximidad y la contención.

Tiempo estimado: 20 minutos

Vea el siguiente vídeo para una breve introducción al laboratorio. [Preparación de datos espaciales](videohub:1_feaq2eu8)

### Objetivos

En esta práctica de prácticas, aprenderá a:

*   Obtener más información y realizar consultas espaciales en Oracle Database

### Requisitos

*   Finalización del laboratorio 3: Preparación de datos espaciales

### Acerca de Consultas Espaciales

Oracle Database incluye una sólida biblioteca de funciones y operadores para el análisis espacial. Esto incluye relaciones espaciales, mediciones, agregaciones, transformaciones y mucho más. Se puede acceder a estas operaciones mediante SQL nativo, PL/SQL, API de Java y cualquier otro lenguaje con módulos de conexión a Oracle como Python y Node.js.

Las operaciones más comunes son operadores espaciales que realizan filtrado y unión espaciales, y funciones espaciales que realizan cálculos y transformaciones.

Los operadores espaciales prueban una relación espacial, como INSIDE o WITHIN\_DISTANCE y devuelven 'TRUE' cuando existe la relación. Los operadores espaciales se utilizan en la cláusula WHERE de una consulta. De forma genérica:

    <code>
    SELECT [fields]
    FROM [tables]
    WHERE [Spatial Operator]='TRUE'
    AND [other conditions...]
    </code>
    

Por ejemplo, para identificar los elementos de MY\_POINTS que están dentro de REGION-01 de MY\_REGIONS:

    <code>
    SELECT *
    FROM MY_POINTS A, MY_REGIONS B
    WHERE SDO_INSIDE(A.GEOMETRY, B.GEOMETRY) = 'TRUE'
    AND B.NAME='MY_REGION-01';
    </code>
    

Las funciones espaciales devuelven un valor y pueden estar en la lista SELECT o utilizarse en la cláusula WHERE. De forma genérica:

    <code>
    SELECT [Spatial Function], [other fields...]
    FROM [tables]
    WHERE [conditions]
    </code>
    

Por ejemplo, para obtener el área REGION-01 de MY\_REGIONS:

    <code>
    SELECT SDO_GEOM.SDO_AREA(GEOMETRY)
    FROM MY_REGIONS
    WHERE NAME='MY_REGION-01';
    </code>
    

Hay cientos de operaciones SQL y PL/SQL espaciales disponibles, como se ha documentado [aquí](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl/spatial-reference-information.html). Explorará algunos de los más comunes de este laboratorio.

### Objetivos

En este laboratorio, realizará consultas espaciales para identificar las relaciones de ubicación entre tiendas, almacenes, regiones y rutas de tornados.

### Requisitos

*   Finalización del laboratorio 3: Preparación de datos espaciales

## Tarea 1: Consultas de proximidad

La proximidad se relaciona con la cercanía entre los elementos. Los dos principales operadores de proximidad espacial son

*   SDO\_WITH\_DISTANCE( ) devuelve elementos dentro de una distancia determinada de otro elemento
*   SDO\_NN( ) devuelve los elementos más cercanos a otro elemento.

1.  Comience por identificar las tiendas dentro de las 20 millas del almacén de Dallas mediante **SDO\_WITHIN\_DISTANCE( )**. Observe que el primer argumento para **SDO\_WITHIN\_DISTANCE( )** es la función que devuelve la geometría para STORES (en lugar de una columna de geometría). Puede utilizar esto desde que creó un índice espacial basado en funciones asociado.
    
        <copy> 
         SELECT
             STORE_NAME,
             STORE_TYPE
         FROM
             STORES     A,
             WAREHOUSES B
         WHERE
              B.WAREHOUSE_NAME = 'Dallas Warehouse'
         AND SDO_WITHIN_DISTANCE(
               GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
               B.GEOMETRY,
               'distance=20 unit=mile') = 'TRUE'
        </copy>
        
    
    ![Consulta de proximidad](images/run-queries-01.png)
    
2.  La identificación de los elementos más cercanos a otro elemento se realiza con el operador espacial **SDO\_NN( )**, donde NN significa vecino más cercano. Ejecute la siguiente consulta para identificar las 5 tiendas más cercanas a Dallas Warehouse. De nuevo, observe que el primer argumento para **SDO\_NN( )** es la función que devuelve la geometría, que tiene un índice espacial basado en funciones.
    
        <copy> 
         SELECT
              STORE_NAME,
              STORE_TYPE
          FROM
              STORES     A,
              WAREHOUSES B
          WHERE B.WAREHOUSE_NAME = 'Dallas Warehouse'
           AND SDO_NN(
                GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                B.GEOMETRY,
                'sdo_batch_size=10') = 'TRUE'
         AND ROWNUM <= 5;
        </copy>
        
    
    ![Consulta de proximidad](images/run-queries-02.png)
    
3.  El operador **SDO\_NN( )** permite incluir la distancia. Ejecute la siguiente consulta para devolver las 5 tiendas más cercanas al almacén de Dallas junto con sus distancias en millas.
    
        <copy> 
         SELECT
              STORE_NAME,
              STORE_TYPE,
              ROUND( SDO_NN_DISTANCE(1) , 2) DISTANCE_MI
          FROM
              STORES     A,
              WAREHOUSES B
          WHERE B.WAREHOUSE_NAME = 'Dallas Warehouse'
           AND SDO_NN(
                GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                B.GEOMETRY,
                'sdo_batch_size=10 unit=MILE', 1) = 'TRUE'
         AND ROWNUM <= 5;
        </copy>
        
    
    ![Consulta de proximidad](images/run-queries-03.png)
    
4.  Ejecute la siguiente consulta para devolver las 5 tiendas minoristas más cercanas al almacén de Dallas junto con sus distancias en millas. Observe que el resultado incluye tiendas más alejadas del resultado anterior, ya que solo está buscando tiendas minoristas.
    
        <copy> 
         SELECT
              STORE_NAME,
              STORE_TYPE,
              ROUND( SDO_NN_DISTANCE(1) , 2) DISTANCE_MI
          FROM
              STORES     A,
              WAREHOUSES B
          WHERE B.WAREHOUSE_NAME = 'Dallas Warehouse'
          AND A.STORE_TYPE='RETAIL'
           AND SDO_NN(
                GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                B.GEOMETRY,
                'sdo_batch_size=10 unit=MILE', 1) = 'TRUE'
         AND ROWNUM <= 5;
        </copy>
        
    
    ![Consulta de proximidad](images/run-queries-04.png)
    
5.  Los operadores espaciales como SDO\_NN( ) también se pueden utilizar para crear una unión. Ejecute la siguiente consulta para devolver cada tienda con el nombre del almacén más cercano.
    
        <copy> 
          SELECT a.store_name, b.warehouse_name
          FROM stores a,warehouses b
          WHERE SDO_NN(b.geometry,
                  get_geometry(a.longitude,a.latitude), 
                  'sdo_num_res=1') = 'TRUE';
        </copy>
        

![Consulta de proximidad](images/run-queries-05.png)

4.  Ejecute la siguiente consulta para devolver cada tienda con el nombre del almacén más cercano junto con las distancias en millas.
    
        <copy> 
          SELECT
              A.STORE_NAME,
              B.WAREHOUSE_NAME,
              ROUND( SDO_NN_DISTANCE(1) , 2) DISTANCE_MI
          FROM
              STORES     A,
              WAREHOUSES B
          WHERE
              SDO_NN(B.GEOMETRY,
                     GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                     'sdo_num_res=1 unit=MILE', 1) = 'TRUE';
        </copy>
        

![Consulta de proximidad](images/run-queries-06.png)

4.  La proximidad es útil para el análisis agregado. Ejecute la siguiente consulta para devolver el número de tornados y la pérdida máxima dentro de las 20 millas del almacén de Dallas.
    
        <copy> 
           SELECT
               COUNT(A.KEY),
               MAX(A.LOSS)
           FROM
               TORNADO_PATHS A,
               WAREHOUSES B
           WHERE
               B.WAREHOUSE_NAME = 'Dallas Warehouse'
            AND SDO_WITHIN_DISTANCE( A.GEOMETRY,
                                     B.GEOMETRY,
                  'distance=20 unit=mile') = 'TRUE'
        </copy>
        
    
    ![Consulta de proximidad](images/run-queries-07.png)
    
    1.  Volviendo al uso de operadores espaciales para uniones, ejecute la siguiente consulta para devolver cada almacén con el número de tornados y la pérdida máxima dentro de 20 millas.
    
        <copy> 
           SELECT
               B.WAREHOUSE_NAME,
               COUNT(A.KEY),
               MAX(A.LOSS)
           FROM
               TORNADO_PATHS A,
               WAREHOUSES B
           WHERE SDO_WITHIN_DISTANCE( A.GEOMETRY,
                                     B.GEOMETRY,
                  'distance=20 unit=mile') = 'TRUE'
           GROUP BY B.WAREHOUSE_NAME;  
        </copy>
        
    
    ![Consulta de proximidad](images/run-queries-08.png)
    

Aumente el valor de distancia en la consulta de 20 a 50 millas y observe el nuevo resultado.

## Tarea 2: Consultas de contención

La contención se refiere a la identificación de elementos que contiene una región específica y viceversa, la identificación de regiones que contienen elementos específicos. Los principales operadores de contención espacial son:

*   SDO\_INSIDE( ) devuelve elementos que están dentro de regiones. Los elementos del límite no se devuelven.
*   SDO\_CONTAINS( ) devuelve regiones que contienen elementos. Los elementos de la frontera no se consideran contenidos.
*   SDO\_ANYINTERACT( ) devuelve elementos que tienen cualquier relación espacial con otros elementos, incluidos los elementos de un límite o elementos parcialmente contenidos, como una línea que se cruza a una región.

1.  Utilice SDO\_INSIDE( ) para devolver tiendas en REGION-02, sin incluir las tiendas en el límite.
    
        <copy> 
          SELECT
              A.STORE_NAME,
              A.STORE_TYPE
          FROM
              STORES  A,
              REGIONS B
          WHERE REGION = 'REGION-02'
          AND SDO_INSIDE(
                 GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                 B.GEOMETRY) = 'TRUE';
         </copy>
        
    
    ![Consulta de contención](images/run-queries-09.png)
    
2.  Utilice SDO\_INSIDE( ) para devolver cada almacén con la región que contiene. Este es otro ejemplo de uso de un operador espacial para realizar una unión, como lo hizo anteriormente con SDO\_NN( ). Tenga en cuenta que no se incluyen las tiendas en un límite de región. Para incluir tiendas en el límite, debe utilizar SDO\_ANYINTERACT( ).
    
        <copy> 
        SELECT
              A.STORE_NAME,
              A.STORE_TYPE,
              B.REGION
          FROM
              STORES  A,
              REGIONS B
          WHERE SDO_INSIDE(
                GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                B.GEOMETRY) = 'TRUE';
         </copy>
        
    
    ![Consulta de contención](images/run-queries-10.png)
    
3.  A continuación, utilice SDO\_ANYINTERACT( ) para agregar tornados por región. Ejecute lo siguiente para devolver el número de tornados y la pérdida máxima para cada región. Tenga en cuenta que SDO\_ANYINTERACT( ) devuelve elementos que tienen alguna relación espacial, como rutas de tornado que una región contiene total o parcialmente.
    
        <copy> 
        SELECT
            B.REGION,
            COUNT(*),
            MAX(LOSS)
        FROM
            TORNADO_PATHS A,
            REGIONS       B
        WHERE
            SDO_ANYINTERACT(A.GEOMETRY, B.GEOMETRY) = 'TRUE'
        GROUP BY
            REGION
        ORDER BY
            REGION;
        </copy>
        
    
    ![Consulta de contención](images/run-queries-11.png)
    
4.  Identifique las regiones que contengan tornados con pérdidas superiores a 100.000 dólares.
    
        <copy> 
          SELECT DISTINCT
              A.REGION
          FROM
              REGIONS       A,
              TORNADO_PATHS B
          WHERE
                 SDO_CONTAINS(A.GEOMETRY, B.GEOMETRY) = 'TRUE'
          AND 
                 B.LOSS > 100000
          ORDER BY
              REGION;
        </copy>
        
    
    ![Consulta de contención](images/run-queries-12.png)
    
5.  Identifique las regiones que contengan tornados con pérdidas superiores a 100.000 dólares junto con el número total de tornados.
    
        <copy> 
          SELECT DISTINCT
              A.REGION,
              COUNT(B.KEY)
          FROM
              REGIONS       A,
              TORNADO_PATHS B
          WHERE
                  SDO_CONTAINS(A.GEOMETRY, B.GEOMETRY) = 'TRUE'
              AND B.LOSS > 100000
          GROUP BY
              REGION
          ORDER BY
              REGION;
        </copy>
        
    
    ![Consulta de contención](images/run-queries-13.png)
    

Ahora puede **proceder al siguiente laboratorio**.

## Más información

*   [Portal de productos espaciales](https://oracle.com/goto/spatial)
*   [Documentación espacial](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Entradas del blog Spatial en Oracle Database Insider](https://blogs.oracle.com/database/category/db-spatial)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Contribuyentes**: Karin Patenge, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, septiembre de 2022