# Restablecer Spatial Studio y ADB al estado anterior al taller

## Introducción

Este laboratorio consiste en eliminar todo lo creado en las prácticas anteriores para que pueda empezar de nuevo si es necesario.

Tiempo de laboratorio estimado: 5 minutos

Vea el siguiente vídeo para una breve introducción al laboratorio.

[Restablecer Spatial Studio y ADB al estado anterior al taller](videohub:1_z4mhzd51)

### Objetivos

En esta práctica de prácticas, aprenderá a:

*   Elimine los artefactos de Spatial Studio y ADB creados en las prácticas anteriores.

### Requisitos

*   Spatial Studio desplegado desde Oracle Cloud Marketplace.

## Tarea 1: Suprimir proyectos

1.  Vaya a la página **Proyectos**. En el menú de acción de Proyectos publicados, seleccione la opción **Suprimir**.
    
    ![Suprimir proyecto publicado](images/reset-01.png)
    
2.  En el menú de acción de Proyectos, seleccione la opción **Suprimir**.
    
    ![Suprimir proyecto](images/reset-02.png)
    

## Tarea 2: Suprimir juegos de datos

1.  Vaya a la página **Conjuntos de datos**. En el menú de acción del juego de datos de análisis **SCHOOLS IN FLOOD2060**, seleccione la opción **Suprimir**.
    
    ![Suprimir juego de datos de análisis espacial](images/reset-03.png)
    
2.  Repita el paso anterior para otros conjuntos de datos de análisis en el siguiente orden: 1) BUILDINGS FLOOD CONTACT, 2) FACILITIES NEAR FLOOD2060 DISTANCE, 3) FACILITIES NEAR FLOOD2060
    
3.  En el menú de acción del juego de datos FACILITIES, seleccione la opción **Delete** (Suprimir).
    
    ![Suprimir juego de datos](images/reset-04.png)
    
4.  En la ventana emergente de confirmación, seleccione la opción para borrar la tabla de base de datos asociada.
    
    ![Confirmar supresión de tabla de base de datos](images/reset-05.png)
    
5.  Repita el proceso para todos los conjuntos de datos restantes.
    

Spatial Studio y ADB ahora se restablecen a su estado previo al taller.

## Más información

*   [Página del producto Oracle Spatial](https://www.oracle.com/database/spatial)
*   [Introducción a Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)
*   [Documentación de Spatial Studio](https://docs.oracle.com/en/database/oracle/spatial-studio)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Contribuyentes**: Denise Myrick
*   **Última actualización por/fecha**: David Lapp, agosto de 2023