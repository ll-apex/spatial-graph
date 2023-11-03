# Crear un gráfico

## Introducción

En esta práctica, creará un gráfico a partir de las tablas `bank_accounts` y `bank_txns` mediante Graph Studio y la sentencia CREATE PROPERTY GRAPH.

Tiempo estimado: 15 minutos.

Vea el siguiente vídeo para una breve introducción al laboratorio. [Tutorial](videohub:1_j5xjw77c)

### Objetivos

Información sobre cómo

*   Utilizar Graph Studio y PGQL DDL (es decir, la sentencia CREATE PROPERTY GRAPH) para modelar y crear un gráfico a partir de tablas o vistas existentes.

### Requisitos

*   En la siguiente práctica se necesita una cuenta de Autonomous Database - Shared Infrastructure.
*   Y que existe el usuario activado para gráficos (`GRAPHUSER`). Es decir, existe un usuario de base de datos con los roles y privilegios correctos.

## Tarea 1: Crear un gráfico de cuentas y transacciones

1.  Haga clic en el icono **Gráfico** para navegar y crear el gráfico.  
    A continuación, haga clic en **Crear gráfico**.
    
    ![Muestra dónde está el modelador de botón de creación](images/graph-create-button.png " ")
    
2.  Introduzca `bank_graph` como nombre del gráfico y, a continuación, haga clic en **siguiente**. Los campos de descripción y etiquetas son opcionales.  
    Ese nombre de gráfico se utiliza en el siguiente ejercicio práctico.  
    No introduzca un nombre diferente porque, a continuación, las consultas y los fragmentos de código de la siguiente práctica de laboratorio fallarán.
    
    ![Muestra la ventana de creación de gráfico en la que se asigna un nombre al gráfico](./images/create-graph-dialog.png " ")
    
3.  Amplíe **GRAPHUSER** y seleccione las tablas `BANK_ACCOUNTS` y `BANK_TXNS`.
    
    ![Muestra cómo seleccionar BANK_ACCOUNTS y BANK_TXNS](./images/select-tables.png " ")
    
4.  Muévalos a la derecha, es decir, haga clic en el primer icono del control de lanzadera.
    
    ![Muestra las tablas seleccionadas](./images/selected-tables.png " ")
    
5.  Haga clic en **Siguiente**. Editaremos y actualizaremos este gráfico para agregar un borde y una etiqueta de vértice.
    
    El gráfico sugerido tiene `BANK_ACCOUNTS` como tabla de vértices, ya que hay restricciones de clave ajena especificadas en `BANK_TXNS` que hacen referencia a él.
    
    Y `BANK_TXNS` es una tabla de perímetro sugerida.
    
    ![Muestra el vértice y la tabla de aristas](./images/create-graph-suggested-model.png " ")
    
6.  Ahora cambiemos las etiquetas Vertex y Edge predeterminadas.
    
    Haga clic en la tabla de vértices `BANK_ACCOUNTS`. Cambie la etiqueta Vertex a **ACCOUNTS**. A continuación, haga clic en la marca de verificación para confirmar la etiqueta y guardar la actualización.
    
    ![Se cambió el nombre de la etiqueta del vértice a Cuentas](images/edit-accounts-vertex-label.png " ")
    
    Haga clic en la tabla de perímetro `BANK_TXNS` y cambie el nombre de la etiqueta de perímetro de `BANK_TXNS` a **TRANSFERS**. A continuación, haga clic en la marca de verificación para confirmar la etiqueta y guardar la actualización.
    
    ![Se ha cambiado el nombre de la etiqueta del borde a Transferencias](images/edit-edge-label.png " ")
    
    Esto es **importante** porque utilizaremos estas etiquetas de borde en la siguiente práctica de este taller al consultar el gráfico. Haga clic en **Siguiente**.
    

7.  En el paso Resumen, haga clic en **Crear gráfico**. Esto abrirá una pestaña Crear gráfico, haga clic en \*\*Crear gráfico.
    
    ![Muestra el separador Trabajo con el estado Correcto](./images/jobs-create-graph.png " ")
    
    Se abrirá un separador Create Graph y, a continuación, haga clic en **Create Graph**.
    
    ![Muestra la función en memoria activada y el botón Crear gráfico](./images/create-graph-in-memory.png " ")
    
    Después de esto, accederá a la página Jobs, donde se creará el gráfico.
    
    Esto concluye este laboratorio. **Ahora puede continuar con la siguiente práctica de laboratorio.**
    

## Reconocimientos

*   **Autor**: Jayant Sharma, gestión de productos
*   **Contribuyentes**: Jayant Sharma, gestión de productos
*   **Última actualización por/fecha**: Ramu Murakami Gutiérrez, mánager de productos, junio de 2023