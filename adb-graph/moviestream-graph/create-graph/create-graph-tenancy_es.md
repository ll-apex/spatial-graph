# Crear un gráfico

## Introducción

En este laboratorio, creará un gráfico a partir de las tablas `MOVIE, CUSTOMER\_SAMPLE` y `WATCHED` mediante la experiencia de usuario guiada de Graph Studio.

Tiempo estimado: 15 minutos.

### Objetivos

Información sobre cómo

*   Utilizar Graph Studio para modelar y crear un gráfico a partir de tablas o vistas existentes.

### Requisitos

*   El siguiente ejercicio práctico requiere una instancia sin servidor de Autonomous Database.
*   Y que el usuario activado para gráficos existe. Es decir, existe un usuario de base de datos con los roles y privilegios correctos.

## Tarea 1: Acceso a Autonomous Database

1.  Haga clic en el **menú de navegación** en la parte superior izquierda, vaya a **Oracle Database** y seleccione **Autonomous Database**.
    
    ![Navegación a Autonomous Database.](images/navigation-menu.png " ")
    
2.  Seleccione el **compartimento** y haga clic en el **nombre mostrado** de **Autonomous Database**.
    
    ![Selección de Autonomous Database en el menú de navegación.](images/select-autonomous-database.png " ")
    

## Tarea 2: Conexión a Graph Studio

[](include:adb-goto-graph-studio.md)

## Tarea 3: Crear un gráfico de recomendaciones de película

[](include:adb-create-graph.md)

## Reconocimientos

*   **Autor**: Melli Annamalai, mánager de productos, Oracle Spatial and Graph
*   **Contribuyentes**: Jayant Sharma
*   **Última actualización por/fecha**: Ramu Murakami Gutiérrez, mánager de productos de Oracle Spatial and Graph, julio de 2023.