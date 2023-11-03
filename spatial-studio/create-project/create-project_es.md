# Crear proyecto

## Introducción

En Spatial Studio, un proyecto es donde visualizas y analizas tus datos. Los proyectos se pueden guardar para que pueda reanudar el trabajo y se pueden publicar para que pueda compartir los resultados con otros. En esta práctica, creará y guardará su primer proyecto.

Tiempo de laboratorio estimado: 30 minutos

### Objetivos

*   Aprender a crear y guardar un proyecto
*   Aprender a agregar juegos de datos a un proyecto
*   Aprende a visualizar conjuntos de datos

### Requisitos

*   Laboratorio 1: Carga de datos espaciales correcta

## Tarea 1: Crear un proyecto

1.  En el menú del panel izquierdo, vaya a la página Proyectos y haga clic en **Crear proyecto**. ![Crear proyecto](images/create-proj-1.png)
    
2.  Haga clic en el botón **Agregar juego de datos** y seleccione **Agregar juego de datos**. ![Agregar juego de datos](images/create-proj-2.png)
    
3.  Seleccione Accidentes y haga clic en **Aceptar**. ![Seleccionar accidentes](images/create-proj-3.png)
    
4.  Arrastre y suelte el juego de datos ACCIDENTS en el mapa. Esto crea una capa de mapa.
    
    **Nota:** Para desplazarse por el mapa, puede utilizar la rueda del mouse para acercar/alejar y hacer clic y arrastrar para desplazarse. ![Arrastre y suelte el juego de datos](images/create-proj-4.png)
    
5.  Opcionalmente, puede configurar los valores de mapa, como una etiqueta, un widget de control de navegación, una barra de escala y una leyenda. Haga clic en el icono de engranaje para acceder a la configuración del mapa. Seleccione las opciones y haga clic en **Aceptar** para activar las selecciones. ![Revisión de icono](images/create-proj-4-1.png) Puede mantener estos cambios o volver a Configuración y desactivar las opciones.
    
6.  En el panel Lista de capas, haga clic en el icono de hamburguesa de Accidentes y seleccione Configuración. ![Seleccionar configuración de la lista de capas](images/create-proj-5.png)
    
7.  Desde aquí se controla la visualización de capas y la configuración de interactividad. Podrá experimentar con estas capacidades en una sección posterior. Por el momento, simplemente actualice el radio (tamaño), el color y la opacidad de la capa y, a continuación, haga clic en el enlace **Atrás**. ![Controlar la visualización de la capa](images/create-proj-6.png)
    

## Tarea 2: Agregar juegos de datos

1.  A continuación, agregue sus 2 conjuntos de datos de policía al proyecto. Haga clic en el botón **Add Dataset** (Agregar juego de datos) en la parte superior del panel Data Elements (Elementos de datos), seleccione **Add Dataset** (Agregar juego de datos), use shift-enter (Intro) para seleccionar ambos juegos de datos de policía y haga clic en **OK** (Aceptar). ![Agregar juego de datos](images/create-proj-7.png)
    
2.  Como ha hecho anteriormente con ACCIDENTS, arrastre y suelte el juego de datos POLICE\_POINTS desde el panel Elementos de datos en el menú de acción de la capa POLICE\_POINT y seleccione Configuración. Actualizar radio, color, opacidad. A continuación, haga clic en el enlace **Atrás** en la parte superior del panel Capas. ![Arrastrar y soltar juego de datos de puntos de policía](images/create-proj-8.png)
    
3.  A medida que se agregan capas al mapa, se representan sobre las capas existentes. Por lo tanto, POLICE\_POINTS está actualmente sobre ACCIDENTS. Para reordenar las capas de modo que POLICE\_POINTS estén debajo de ACCIDENTS, mueva el mouse sobre POLICE\_POINTS en la lista de la capa, haga clic y mantenga pulsado (verá que el cursor cambia a cross-hair) y arrástrelo debajo de ACCIDENTS. ![Reordenar capas](images/create-proj-9.png)
    
4.  Arrastre y suelte el juego de datos POLICE\_BOUNDS en el mapa. Como hizo con POLICE\_POINTS, vuelva a ordenar las capas para que POLICE\_BOUNDS esté en la parte inferior (es decir, representado debajo de las otras capas). Ahora tiene sus 3 conjuntos de datos agregados como capas de mapa en nuestro proyecto.
    

**Nota:** Las capas individuales se pueden desactivar o activar haciendo clic en el icono de globo ocular situado junto al nombre de la capa.

![Arrastrar y soltar juego de datos de límites de policía](images/create-proj-10.png)

5.  Haga clic en el menú de hamburguesa de la capa POLICE\_BOUNDS y seleccione Settings. Actualizar color y opacidad para el relleno y el esquema. Observe que el uso de un contorno blanco reduce el efecto desordenado de un contorno más oscuro. ![Alternar capas individuales](images/create-proj-11.png)

Haga clic en el enlace **Atrás** en la parte superior del panel Configuración de capa para volver a la lista Capas.

## Tarea 3: Adición de visualizaciones

1.  Spatial Studio le permite mostrar sus conjuntos de datos como mapas y tablas. Para agregar visualizaciones, haga clic en el separador **Visualizaciones** de la izquierda y, a continuación, arrastre y suelte la **tabla** en el borde de la vista de mapa existente. Aparecerá una barra gris cuando se pueda colocar la tabla.

![Agregar vista de tabla](images/add-viz-1.png)

2.  Arrastre y suelte **Mapa** sobre el mapa existente. La barra gris aparecerá al pasar el cursor sobre el borde del mapa existente y puede caer en el nuevo mapa.

![Agregar nueva vista de mapa](images/add-viz-2.png)

3.  Haga clic en el botón **Datasets** (Conjuntos de datos) en la parte superior izquierda y, a continuación, arrastre y suelte ACCIDENTS (ACIDENTES) en la tabla.

![Agregar juego de datos de accidentes a vista de tabla](images/add-viz-3.png)

4.  Arrastre y suelte ACCIDENTES en el nuevo mapa.

![Agregar juego de datos Accidentes a nueva vista de mapa](images/add-viz-4.png)

5.  Para contraer el panel Elementos de datos y proporcionar más propiedades de pantalla, desplácese sobre el borde derecho y haga clic en la flecha gris.

![Contraer el panel Elementos de datos](images/add-viz-5.png)

6.  Para expandir el panel Elementos de datos, desplácese sobre el borde izquierdo y haga clic en la flecha gris.

![Ampliar el panel Elementos de Datos](images/add-viz-6.png)

7.  Para suprimir una visualización, haga clic en el icono **X** en la parte superior derecha. Utilizaremos solo nuestro mapa inicial en este taller, así que elimine la nueva tabla y el mapa que acaba de crear.

![Suprimir una visualización](images/add-viz-7.png)

## Tarea 4: Guardar proyecto

1.  Haga clic en el botón **Guardar** en la parte superior derecha para guardar el proyecto y proporcionar un nombre, por ejemplo, **LiveLabs Introducción espacial**. ![Guardar proyecto](images/create-proj-12.png)
    
2.  Vaya a la página Projects desde la barra de navegación izquierda y observe que su proyecto ahora aparece. ![Ver lista de proyectos](images/create-proj-13.png)
    

Ahora puede [proceder al siguiente laboratorio](#next).

## Más información

*   \[Portal de productos de Spatial Studio\] (https://oracle.com/goto/spatialstudio)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: Denise Myrick, Database Product Management, abril de 2023