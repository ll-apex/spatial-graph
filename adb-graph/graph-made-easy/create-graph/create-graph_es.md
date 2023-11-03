# Crear un gráfico

## Introducción

En esta práctica, creará un gráfico a partir de las tablas `bank_accounts` y `bank_txns` mediante Graph Studio y la sentencia CREATE PROPERTY GRAPH.

Tiempo estimado: 15 minutos.

Vea el siguiente vídeo para una breve introducción al laboratorio. [Creación de un gráfico de propiedades en Graph Studio](videohub:1_cz3cwg3h)

### Objetivos

Información sobre cómo

*   Utilizar Graph Studio y PGQL DDL (es decir, la sentencia CREATE PROPERTY GRAPH) para modelar y crear un gráfico a partir de tablas o vistas existentes.

### Requisitos

*   En la siguiente práctica se necesita una cuenta de Autonomous Database - Shared Infrastructure.
*   Y que existe el usuario activado para gráficos (`GRAPHUSER`). Es decir, existe un usuario de base de datos con los roles y privilegios correctos.

## Tarea 1: Crear un gráfico de cuentas y transacciones a partir de las tablas correspondientes

1.  Haga clic en el icono **Gráfico** para navegar y crear el gráfico.  
    A continuación, haga clic en **Crear**.  
    ![Muestra dónde está el modelador de botón de creación](images/graph-create-button.png " ")
    
2.  A continuación, seleccione las tablas `BANK_ACCOUNTS` y `BANK_TXNS`.  
    ![Muestra cómo seleccionar BANK_ACCOUNTS y BANK_TXNS](./images/select-tables.png " ")
    
3.  Muévalos a la derecha, es decir, haga clic en el primer icono del control de lanzadera.
    

![Muestra las tablas seleccionadas](./images/selected-tables.png " ")

4.  Haga clic en **Siguiente** para obtener un modelo sugerido. Editaremos y actualizaremos este modelo para agregar un borde y una etiqueta de vértice.
    
    El modelo sugerido tiene `BANK_ACCOUNTS` como tabla de vértices, ya que hay restricciones de clave ajena especificadas en `BANK_TXNS` que hacen referencia a él.
    
    Y `BANK_TXNS` es una tabla de perímetro sugerida.
    

![Muestra el vértice y la tabla de aristas](./images/create-graph-suggested-model.png " ")

5.  Ahora cambiemos las etiquetas Vertex y Edge predeterminadas.
    
    Haga clic en la tabla de vértices `BANK_ACCOUNTS`. Cambie la etiqueta Vertex a **ACCOUNTS**. A continuación, haga clic fuera del cuadro de entrada en la etiqueta de confirmación y guarde la actualización.
    
    ![Se cambió el nombre de la etiqueta del vértice a Cuentas](images/edit-accounts-vertex-label.png " ")
    
    Haga clic en la tabla de perímetro `BANK_TXNS` y cambie el nombre de la etiqueta de perímetro de `BANK_TXNS` a **TRANSFERS**.  
    A continuación, haga clic fuera del cuadro de entrada de la etiqueta de confirmación y guarde la actualización.
    
    ![Se ha cambiado el nombre de la etiqueta del borde a Transferencias](images/edit-edge-label.png " ")
    
    Esto es **importante** porque utilizaremos estas etiquetas de borde en la siguiente práctica de este taller al consultar el gráfico.
    
6.  Como se trata de bordes dirigidos, se recomienda verificar que la dirección es correcta.  
    En esta instancia, queremos **confirmar** que la dirección va de `from_acct_id` a `to_acct_id`.
    
    > **Nota:** La información `Source Vertex` y `Destination Vertex` de la izquierda.
    
    ![Muestra cómo la dirección del vértice es incorrecta](images/wrong-edge-direction.png " ")
    
    **Observe** que la dirección es incorrecta. La clave de origen es `to_acct_id` en lugar de lo que queremos, que es `from_acct_id`.
    
    Haga clic en el icono del borde de intercambio situado a la derecha para intercambiar los vértices de origen y destino y, por lo tanto, invertir la dirección del borde.
    
    > **Nota:** `Source Vertex` es ahora el correcto, es decir, `FROM_ACCT_ID`.
    
    ![Muestra cómo la dirección es correcta](images/reverse-edge-result.png " ")
    
7.  Haga clic en el separador **Origen** para verificar que la dirección del borde y, por lo tanto, la sentencia CREATE PROPERTY GRAPH generada sean correctas.
    
    ![Verifica que la dirección del borde es correcta en el origen](images/generated-cpg-statement.png " ")
    

8.  Haga clic en **Siguiente** y, a continuación, en **Crear gráfico** para ir al siguiente paso del flujo.
    
    Introduzca `bank_graph` como nombre del gráfico.  
    Ese nombre de gráfico se utiliza en el siguiente ejercicio práctico.  
    No introduzca un nombre diferente porque, a continuación, las consultas y los fragmentos de código de la siguiente práctica de laboratorio fallarán.
    
    Introduzca un nombre de modelo (por ejemplo, `bank_graph_model`) y otra información opcional y, a continuación, haga clic en Create. ![Muestra la ventana de creación de gráfico en la que se asigna un nombre al gráfico](./images/create-graph-dialog.png " ")
    
9.  Graph Studio modeler ahora guardará los metadatos e iniciará un trabajo para crear el gráfico.  
    La página Trabajos muestra el estado de este trabajo.
    
    ![Muestra el separador Trabajo con el estado Correcto](./images/jobs-create-graph.png " ")
    
    A continuación, puede consultar y visualizar el gráfico de forma interactiva en un bloc de notas después de cargarlo en la memoria.
    

Esto concluye este laboratorio. **Ahora puede continuar con la siguiente práctica de laboratorio.**

## Reconocimientos

*   **Autor**: Jayant Sharma, gestión de productos
*   **Contribuyentes**: Jayant Sharma, gestión de productos
*   **Última actualización por/fecha**: Ramu Murakami Gutiérrez, gestión de productos, junio de 2022