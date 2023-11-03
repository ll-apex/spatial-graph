# Crear datos de ejemplo

## Introducción

En este laboratorio se muestran los pasos para crear datos espaciales de ejemplo en Oracle Database.

Tiempo de laboratorio estimado: 10 minutos

### Objetivos

En esta práctica de prácticas, aprenderá a:

*   Más información sobre la gestión de datos espaciales en Oracle Database
*   Preparar datos espaciales en Oracle Database a partir de formatos de archivo comunes

### Requisitos

*   Finalización del laboratorio 2

### Acerca de los datos espaciales

Oracle Database almacena datos espaciales (puntos, líneas, polígonos) en un tipo de dato nativo denominado SDO\_GEOMETRY. Oracle Database también proporciona un índice espacial nativo para operaciones espaciales de alto rendimiento. Este índice espacial se basa en metadatos espaciales que se introducen para cada tabla y columna de geometría que almacena datos espaciales. Una vez que los datos espaciales se rellenan e indexan, hay API sólidas disponibles para realizar análisis, cálculos y procesamiento espaciales.

El tipo SDO\_GEOMETRY tiene el siguiente formato general:

    SDO_GEOMETRY( 
     [geometry type],           --ID for point/line/polygon
     [coordinate system],       --ID of coordinate system
     [point coordinate],        --for points only
     [line/polygon info],       --for lines/polygons only
     [line/polygon coordinates] --for lines/polygons only
      )
    

Los tipos de geometría más comunes son 2 dimensiones:

| ID | Tipo |
| --- | --- |
| 2001 | Punto |
| 2002 | Línea |
| 2003 | Polígono |

Los sistemas de coordenadas más comunes son:

| ID | Sistema de Coordenadas |
| --- | --- |
| 4326 | Latitud/longitud |
| 3857 | World Mercator |

Al utilizar la latitud/longitud, tenga en cuenta que la latitud es la coordenada Y y la longitud es la coordenada X. Dado que las coordenadas se muestran como par X, Y, los valores están realmente en la longitud de orden, latitud.

A continuación se muestra un ejemplo de geometría de punto mediante coordenadas de latitud/longitud:

    SDO_GEOMETRY( 
     2001,               --2D point
     4326,               --latitude/longitude
     SDO_POINT_TYPE(     
        -100.123, 20.456 --coordinate
        ),         
     NULL,               --for lines/polygons only
     NULL                --for lines/polygons only
      )
    

A continuación se muestra un ejemplo de geometría de polígono que utiliza coordenadas de latitud/longitud:

    SDO_GEOMETRY( 
     2003,                  --2D polygon
     4326,                  --latitude/longitude
     NULL,                  --for points only       
     SDO_ELEM_INFO_ARRAY(
          1, 1003, 1        --indicates simple exterior polygon
            ), 
     SDO_ORDINATE_ARRAY(   
        -98.789065,39.90973, -- coordinates
        -101.2522,39.639537,
        -99.84374,37.160316,
        -96.67987,35.460699,
        -94.21875,39.639537,
        -98.789025,39.90973
          )
        )
    );
    

### Objetivos

En esta práctica de prácticas, aprenderá a:

*   Crear tablas con una columna de geometría
*   Rellenar geometrías
*   Crear metadatos e índices espaciales

### Requisitos

Como se describe en la introducción del taller, necesita acceso a Oracle Database y SQL Client. Si no tiene estos, vuelva a las secciones de Oracle Cloud Account, Autonomous Database y SQL Developer Web.

## Tarea 1: Crear tablas con coordenadas

Comenzamos creando tablas con coordenadas de latitud y longitud. Este es un punto de partida común para crear datos espaciales, por ejemplo, coordenadas de GPS, o de dirección postal o dirección IP de geocodificación.

Las instrucciones y capturas de pantalla hacen referencia a SQL Developer Web; sin embargo, los mismos pasos se aplican a otros clientes SQL.

1.  Descargue el script SQL [aquí](files/create-sample-data.sql).
    
2.  Copiar/pegar/ejecutar el script en SQL Developer Web ![Texto alternativo de imagen](images/run-script-1.png)
    
3.  Refrescar lista para ver las tablas BRANCHES y WAREHOUSES
    
    ![Texto alternativo de imagen](images/refresh-tables-1.png)
    

## Tarea 2: Crear geometrías a partir de coordenadas

Las geometrías se pueden rellenar con SQL, para casos exathis especificando las coordenadas de geometrías de puntos basadas en columnas de latitud y longitud.

1.  Agregue columnas de geometría:
    
        <copy> 
        ALTER TABLE WAREHOUSES ADD (
         GEOMETRY SDO_GEOMETRY
        );
        
        ALTER TABLE BRANCHES ADD (
           GEOMETRY SDO_GEOMETRY
        );
        </copy>
        
2.  Introducir columnas de geometría:
    
        <copy> 
        UPDATE WAREHOUSES
        SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
         UPDATE BRANCHES
         SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
        </copy>
        

## Tarea 3: Crear tabla con polígono

Las líneas y los polígonos se pueden crear de la misma manera. Mientras que una geometría de punto requiere una coordenada, las líneas y polígonos requieren todas las coordenadas que definen la geometría. En este caso creamos una tabla para almacenar un polígono.

1.  Crear tabla e insertar fila
    
        <copy>
        CREATE TABLE COASTAL_ZONE (
            ZONE_ID   NUMBER,
            GEOMETRY  SDO_GEOMETRY
        );       
        
        INSERT INTO COASTAL_ZONE VALUES (
            1,
            SDO_GEOMETRY(
                2003, 4326, NULL, SDO_ELEM_INFO_ARRAY(
                    1, 1003, 1
                ), SDO_ORDINATE_ARRAY(
                    -93.719934, 30.210638,
                    -95.422592, 29.773714, 
                    -95.059698, 29.322204, 
                    -96.013892, 28.787021, 
                    -96.660964, 28.925638, 
                    -97.528688, 28.042050, 
                    -97.858501, 27.447461, 
                    -97.497364, 25.880056, 
                    -96.977826, 25.969716, 
                    -97.211445, 27.054605, 
                    -96.870226, 27.816077, 
                    -93.794290, 29.535729, 
                    -93.719934, 30.210638
                )
            )
        );
        </copy>
        
2.  Refresque la lista de tablas para ver la tabla COASTAL\_ZONE. ![Texto alternativo de imagen](images/refresh-tables-2.png)
    

## Tarea 4: Agregar índices y metadatos espaciales

Oracle Database proporciona un índice espacial nativo para operaciones espaciales de alto rendimiento. Nuestros datos de muestra son tan pequeños que no se necesita realmente un índice espacial. Sin embargo, realizamos los siguientes pasos, ya que son importantes para volúmenes de datos de producción típicos. Un índice espacial necesita una fila de metadatos para la geometría que se indexa. Creamos estos metadatos y, a continuación, los índices espaciales.

1.  Agregue metadatos espaciales:
    
        <copy> 
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'WAREHOUSES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'BRANCHES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'COASTAL_ZONE',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        </copy>
        
2.  Crear índices espaciales:
    
        <copy> 
        CREATE INDEX WAREHOUSES_SIDX ON
            WAREHOUSES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX BRANCHES_SIDX ON
            BRANCHES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX COASTAL_ZONE_SIDX ON
            COASTAL_ZONE (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
         </copy>
        
    
    Después de crear los índices, refresque la lista de tablas. Verá 3 tablas con nombres que empiezan por MDRT\_. Son artefactos de los índices espaciales que Oracle Database gestiona automáticamente. Nunca debe manipular manualmente estas tablas. ![Texto alternativo de imagen](images/refresh-tables-3.png)
    
    Nuestros datos de muestra ahora están preparados y listos para consultas espaciales.
    
    Ahora puede pasar a la siguiente práctica de laboratorio.
    
    Si necesita revertir esta práctica de laboratorio y eliminar los elementos creados, ejecute lo siguiente:
    
         DROP TABLE BRANCHES;   
         DROP TABLE WAREHOUSES;
         DROP TABLE COASTAL_ZONE;
         DELETE FROM USER_SDO_GEOM_METADATA;
         COMMIT;
        

## Más información

*   \[Portal de productos espaciales\] (https://oracle.com/goto/spatial)
*   [Documentación espacial](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Blogs espaciales](https://blogs.oracle.com/oraclespatial/)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: Kamryn Vinson, noviembre de 2020