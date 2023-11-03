# Restablecer ADB a estado previo al taller

## Introducción

Este laboratorio consiste en eliminar todo lo creado en las prácticas anteriores para que pueda empezar de nuevo si es necesario.

Tiempo de laboratorio estimado: 2 minutos

### Acerca de

En este laboratorio, se borran todos los artefactos creados anteriormente.

### Objetivos

*   Restablezca la ADB al estado anterior al taller.

### Requisitos

*   Finalización del laboratorio 3: Preparación de datos espaciales

## Tarea 1: Eliminar todo lo creado en este taller

1.  Para eliminar tablas e índices creados en este taller, ejecute lo siguiente con el botón Run Script de SQL Worksheet.
    
    ![Texto alternativo de imagen](images/run-script.png)
    
        <copy> 
        DROP TABLE WAREHOUSES;
        DROP TABLE STORES;
        DROP TABLE REGIONS;
        DROP TABLE TORNADO_PATHS;
        </copy>
        
2.  Para borrar los metadatos espaciales insertados en este taller, ejecute lo siguiente con el botón Run Script de SQL Worksheet.
    
        <copy> 
        DELETE FROM USER_SDO_GEOM_METADATA
        WHERE TABLE_NAME IN (
            'WAREHOUSES', 
            'STORES', 
            'REGIONS', 
            'TORNADO_PATHS');
        COMMIT;
        </copy>
        
3.  Para borrar la función creada en este taller, ejecute lo siguiente.
    
        <copy> 
        DROP FUNCTION GET_GEOMETRY;
        </copy>
        

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, septiembre de 2022