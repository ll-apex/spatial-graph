# Consultas espaciales

## Introducción

Este laboratorio le guiará a través de consultas espaciales básicas en Oracle Database. Utilizará los datos de ejemplo creados en el laboratorio anterior para identificar elementos en función de la proximidad y la contención.

Tiempo de laboratorio estimado: 15 minutos

### Acerca de Consultas Espaciales

Oracle Database incluye una sólida biblioteca de funciones y operadores para el análisis espacial. Esto incluye relaciones espaciales, mediciones, agregaciones, transformaciones y mucho más. Se puede acceder a estas operaciones mediante SQL nativo, PL/SQL, API de Java y cualquier otro lenguaje que se comunique con Oracle Database.

### Objetivos

En esta práctica de prácticas, aprenderá a:

*   Identificar BRANCHES que tengan relaciones de proximidad con un ALMACÉN
*   Identificar BRANCHES que tengan relaciones de inclusión y proximidad a COASTAL\_ZONE

### Requisitos

*   Finalización de la práctica de laboratorio anterior; creación de datos espaciales de ejemplo

## Consultas espaciales

Las consultas espaciales de Oracle Database son como cualquier otra consulta tradicional a la que esté acostumbrado. La única diferencia es un conjunto de funciones espaciales y operadores que probablemente sean nuevos para usted.

**Identifique las 5 sucursales más cercanas al almacén de Dallas:**

    <copy> 
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5'
        ) = 'TRUE';
    </copy>
    

![Ejecutar una consulta espacial](images/query1.png) Notas:

*   El operador `SDO_NN` devuelve las ramas 'n más cercanas' al almacén de Dallas, donde 'n' es el valor específico para `SDO_NUM_RES`. El primer argumento para `SDO_NN` (`B.GEOMETRY` en el ejemplo anterior) es la columna que se va a buscar. El segundo argumento (`W.GEOMETRY` en el ejemplo anterior) es la ubicación a la que desea encontrar los vecinos más cercanos. No se deben realizar suposiciones sobre el orden de los resultados devueltos. Por ejemplo, no se garantiza que la primera fila devuelta sea la más cercana. Si dos o más bifurcaciones están a la misma distancia del almacén, se pueden devolver en llamadas posteriores a `SDO_NN`.
*   Al utilizar el parámetro `SDO_NUM_RES`, no se utiliza ningún otro criterio en la cláusula `WHERE`. `SDO_NUM_RES` solo tiene en cuenta la proximidad. Por ejemplo, si ha agregado un criterio a la cláusula `WHERE` porque desea que las cinco bifurcaciones más cercanas tengan un código postal específico y cuatro de las cinco bifurcaciones más cercanas tengan un código postal diferente, la consulta anterior devolvería una fila. Este comportamiento es específico del parámetro `SDO_NUM_RES`. En una consulta siguiente, utilizará un parámetro alternativo para el escenario de criterios de consulta adicionales.

**Identifique las 5 sucursales más cercanas al Almacén de Dallas con la distancia:**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5 unit=km', 1
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Ejecutar una consulta espacial](images/query2.png) Notas:

*   El operador `SDO_NN_DISTANCE` es un operador auxiliar del operador `SDO_NN`; solo se puede utilizar dentro del operador `SDO_NN`. El argumento para este operador es un número que coincide con el número especificado como último argumento de `SDO_NN`; en este ejemplo es 1. No hay un significado oculto para este argumento, es simplemente una etiqueta. Si se especifica `SDO_NN_DISTANCE()`, puede ordenar los resultados por distancia y garantizar que la primera fila devuelta sea la más cercana. Si los datos que consulta se almacenan como longitud y latitud, la unidad por defecto para `SDO_NN_DISTANCE` son los metros.
*   El operador `SDO_NN` también tiene un parámetro `UNIT` que determina la unidad de medida devuelta por `SDO_NN_DISTANCE`.
*   La cláusula `ORDER BY DISTANCE` garantiza que las distancias se devuelvan en orden, con la distancia más corta en primer lugar.

**Identifique las 5 sucursales WHOLESALE más cercanas al Almacén de Dallas con distancia:**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND B.BRANCH_TYPE = 'WHOLESALE'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_batch_size=5 unit=km', 1
        ) = 'TRUE'
        AND ROWNUM <= 5
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Ejecutar una consulta espacial](images/query3.png) Notas:

*   `SDO_BATCH_SIZE` es un parámetro ajustable que puede afectar al rendimiento de la consulta. `SDO_NN` calcula internamente ese número de distancias a la vez. Es posible que el lote inicial de filas devueltas no satisfaga las restricciones de la cláusula WHERE, por lo que el número de filas especificado por `SDO_BATCH_SIZE` se devuelve continuamente hasta que se cumplen todas las restricciones de la cláusula WHERE. Debe seleccionar un `SDO_BATCH_SIZE` que devuelva inicialmente el número de filas que probablemente satisfagan las restricciones en la cláusula WHERE.
*   El parámetro `UNIT` utilizado en el operador `SDO_NN` especifica la unidad de medida del parámetro `SDO_NN_DISTANCE`. La unidad predeterminada es la unidad de medida asociada a los datos. Para los datos de longitud y latitud, el valor por defecto es metros.
*   `B.BRANCH_TYPE = 'WHOLESALE' AND ROWNUM <= 5` son las restricciones adicionales de la cláusula `WHERE`. La cláusula rownum es necesaria para limitar el número de resultados devueltos a 5.
*   La cláusula `ORDER BY DISTANCE_KM` garantiza que las distancias se devuelvan en orden, con la distancia más corta primero y las distancias medidas en millas.

**Identifique las sucursales dentro de los 50km de Houston Warehouse:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE';
    </copy>
    

![Ejecutar una consulta espacial](images/query4.png) Notas:

*   El primer argumento para `SDO_WITHIN_DISTANCE` es la columna que se va a buscar. El segundo argumento es la ubicación desde la que desea determinar las distancias. No se deben realizar suposiciones sobre el orden de los resultados devueltos. Por ejemplo, no se garantiza que la primera fila devuelta sea el cliente más cercano al almacén 3.
*   El parámetro DISTANCE utilizado en el operador `SDO_WITHIN_DISTANCE` especifica el valor de distancia; en este ejemplo es 100.
*   El parámetro UNIT utilizado en el operador `SDO_WITHIN_DISTANCE` especifica la unidad de medida del parámetro DISTANCE. La unidad predeterminada es la unidad de medida asociada a los datos. Para los datos de longitud y latitud, el valor por defecto es metros; en este ejemplo, son millas.

**Identifique las sucursales a 50 km de Houston Warehouse con la distancia:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE,
        ROUND(
            SDO_GEOM.SDO_DISTANCE(
                B.GEOMETRY, W.GEOMETRY, 0.05, 'unit=km'
            ), 2
        ) AS DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Ejecutar una consulta espacial](images/query5.png) Notas:

*   La función `SDO_GEOM.SDO_DISTANCE` calcula la distancia entre las ubicaciones de las sucursales y el almacén de Houston.
*   Los primeros 2 argumentos para `SDO_GEOM.SDO_DISTANCE` son ubicaciones BRANCH y WAREHOUSE para el cálculo de distancia.
*   El tercer argumento para `SDO_GEOM.SDO_DISTANCE` es el valor de tolerancia. La tolerancia es un valor de error de redondeo utilizado por Oracle Spatial. La tolerancia es en metros para los datos de longitud y latitud. En este ejemplo, la tolerancia es de 50 mm.
*   El parámetro UNIT utilizado en el parámetro `SDO_GEOM.SDO_DISTANCE` especifica la unidad de medida de la distancia calculada por la función `SDO_GEOM`.`SDO_DISTANCE`. La unidad predeterminada es la unidad de medida asociada a los datos. Para los datos de longitud y latitud, el valor por defecto es metros. En este ejemplo son las millas.
*   La cláusula `ORDER BY DISTANCE_IN_MILES` garantiza que las distancias se devuelvan en orden, con la distancia más corta primero y las distancias medidas en millas.

**Identifique las ramas de la zona costera:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE';
    </copy>
    

![Ejecutar una consulta espacial](images/query6.png) Notas:

*   El operador `SDO_ANYINTERACT` acepta 2 argumentos, geometry1 y geometry2. El operador devuelve `TRUE` para las filas en las que geometry1 está dentro o en el límite de geometry2.
*   En este ejemplo, geometry1 es `B.GEOMETRY`, las geometrías de rama y geometry2 es `C.GEOMETRY`, la geometría de zona costera. La tabla COASTAL\_ZONE solo tiene 1 fila, por lo que no se necesitan criterios adicionales.

**Identifique las ramas fuera y dentro de los 10 km de la zona costera:**

    <copy>
    
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_WITHIN_DISTANCE(
            B.GEOMETRY, C.GEOMETRY, 'distance=10 unit=km'
        ) = 'TRUE'
    )
    MINUS
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE'
    );
    </copy>
    

![Ejecutar una consulta espacial](images/query7.png) Notas:

*   En la primera parte de esta consulta, el operador `SDO_WITHIN_DISTANCE` identifica BRANCHES a 10 km de COASTAL\_ZONE. Esto incluye las marcas dentro de COASTAL\_ZONE.
*   La consulta utiliza `MINUS` para eliminar BRANCHES dentro de COASTAL\_ZONE, dejando solo BRACNCHES dentro de 10 km y fuera de COASTAL\_ZONE.

## Más información

*   \[Portal de productos espaciales\] (https://oracle.com/goto/spatial)
*   [Documentación espacial](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Blogs espaciales](https://blogs.oracle.com/oraclespatial/)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: Kamryn Vinson, noviembre de 2020