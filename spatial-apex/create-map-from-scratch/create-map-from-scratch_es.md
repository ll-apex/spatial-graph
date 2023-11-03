# Crear mapa nuevo

## Introducción

En este laboratorio, creará una nueva página en la aplicación y, a continuación, configurará Map Region desde cero.

Tiempo de laboratorio estimado: 15 minutos

### Objetivos

*   Comprender la configuración de la región de mapa de APEX

### Requisitos

*   Laboratorio 2: Crear mapa con asistente

## Tarea 1: Creación de una Nueva Página

1.  En las rutas de navegación de la parte superior izquierda, haga clic en el enlace del directorio raíz de la aplicación. A continuación, haga clic en el separador **Diseño**. ![Diseño de página](images/create-map-15a.png)
    
2.  Haga clic en **Crear Página**. ![Asistente de Creación de Páginas](images/create-map-15b.png)
    
3.  Puede seleccionar Asignar aquí para tener el mismo asistente que ha visto en el asistente Crear aplicación. Pero este paso consiste en crear un mapa desde cero, por ejemplo, si tiene una página existente. Seleccione **Página en blanco** y, a continuación, haga clic en **Siguiente**. ![Seleccionar página en blanco](images/create-map-16.png)
    
4.  Para el nombre, introduzca **Asignación de aeropuertos y estados** y, a continuación, haga clic en **Siguiente**. ![Introducir nombre de página](images/create-map-16a.png)
    
5.  Seleccione la opción para crear una nueva entrada de menú de navegación e introduzca **Asignación de aeropuertos y estados**, es decir, el mismo que el nombre de la página. A continuación, haga clic en **Siguiente**. ![Crear entrada de menú de navegación](images/create-map-17.png)
    
6.  Revise el resumen y haga clic en **Terminar**. ![Revisar resumen](images/create-map-18.png)
    

## Tarea 2: Agregar un mapa a la página

1.  Arrastre **Mapa** desde la paleta Regiones en la parte inferior y suelte bajo la sección Cuerpo del diseño de página. Observe que Map Region aparece en el árbol Page bajo Body con el nombre por defecto New. Haga clic en **Nuevo** en el árbol de páginas y observe sus propiedades a la derecha. Observe que Region Type es Map. ![Agregar Región de Asignación](images/create-map-19.png)
    
2.  En el panel de la derecha, actualice el título de región de Nuevo a un nombre que elija, por ejemplo, **Mi región de mapa**. Observe que el título se actualiza en el árbol de páginas de la izquierda. ![Introducir título de región](images/create-map-20.png)
    
3.  Observe que Map Region incluye un elemento secundario denominado Layers with a default Layer denominado New. Las capas son el contenido basado en datos que se va a representar en el mapa. Haga clic en la capa **Nueva** del árbol de páginas para ver sus propiedades en el panel derecho. ![Ver propiedades de capa](images/create-map-21.png)
    
4.  Actualice el nombre de capa a **Aeropuertos** y el tipo a **Puntos**. Observe la actualización Layer Name en el árbol de páginas de la izquierda. ![Actualizar propiedades de capa](images/create-map-23.png)
    
5.  Desplácese hacia abajo en el panel de propiedades Layer de la derecha. Actualice el **Origen** para utilizar la tabla **EBA\_SAMPLE\_MAP\_AIRPORTS**. Para limitar los aeropuertos representados en la capa, agregue la cláusula where **LAND\_AREA\_COVERED > 2500**. Active la opción Use Spatial Index (Usar índice espacial) con el conmutador. ![Actualizar propiedades de capa](images/create-map-24.png)
    
6.  Desplácese hacia abajo en el panel Propiedades de capa situado a la derecha de la sección **Asignación de columnas**. Aquí es donde se configura la columna espacial para la representación. Seleccione el tipo de dato de geometría **SDO\_GEOMETRY** y la columna de geometría **GEOMETRY**. ![Actualizar propiedades de capa](images/create-map-25.png)
    
7.  Desplácese hacia abajo en el panel Propiedades de capa situado a la derecha de la sección **Ventana de información**. Aquí es donde puede configurar el contenido de una ventana de información que aparece al hacer clic en un elemento del mapa. Active **Formato Avanzado** haciendo clic en el botón de cambio y, a continuación, pegue lo siguiente en el área de texto **Expresión HTML**:
    
        <copy>
        <strong>&AIRPORT_NAME.</strong><br>
        &CITY., &STATE_NAME.<br>
        Code: &IATA_CODE.
        </copy>
        
    
    ![Actualizar propiedades de capa](images/create-map-25a.png)
    

## Tarea 3: Agregar una capa al mapa

1.  En el árbol Página de la izquierda, haga clic con el botón derecho en **Capas** en la región de mapa y seleccione **Crear capa**. ![Agregar una capa](images/create-map-26.png)
    
2.  Haga clic en la capa recién creada en el árbol de páginas de la región de mapa. A continuación, en el panel Detalles de capa de la derecha, actualice el nombre a **Estados**, el tipo de capa a **Polígonos** y el origen a **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES**. ![Actualizar propiedades de capa](images/create-map-27.png)
    
3.  Las capas se representarán en el orden en que aparecen en el árbol de páginas. Para que los aeropuertos se representen en los estados superiores, arrastre la capa **Estados** encima de la capa Aeropuertos en las capas del árbol de páginas. Desplácese hacia abajo en el panel Detalles de capa situado a la derecha de la sección Asignación de columnas. Seleccione el tipo de dato de geometría **SDO\_GEOMETRY** y la columna de geometría **GEOMETRY**. En Apariencia, seleccione los colores de relleno y trazo (esquema) que desee. Establezca la opacidad de relleno en un valor de su elección, señalando que un valor de 1 significa totalmente opaco para que el mapa de fondo no sea visible. ![Actualizar orden de capa](images/create-map-28.png)
    
4.  En la parte superior derecha, haga clic en **Guardar** y, a continuación, en el botón verde **Ejecutar**. ![Guardar y Ejecutar, página](images/create-map-29.png)
    
5.  Observe la representación del mapa con las capas de estados y aeropuertos. Haga clic y arrastre el mapa para desplazarse y utilice el control de navegación situado en la parte superior derecha para acercar y alejar. Haga clic en un aeropuerto para ver la ventana de información que ha configurado. Pase el mouse sobre un estado para ver la pista que configuró. Desactive las capas con las casillas de verificación debajo del mapa. ![Interactuar con el mapa](images/create-map-30.png)
    

Felicidades por crear tu primer mapa desde cero. En el próximo laboratorio incorporará el análisis espacial en este mapa.

Esto concluye el laboratorio. Ahora puede pasar a la siguiente práctica de laboratorio.

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, Database Product Management, marzo de 2023