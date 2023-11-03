# Crear mapa con asistente

## Introducción

Oracle APEX proporciona un asistente para crear una variedad de tipos de páginas útiles. En este laboratorio, utilizará el asistente para crear una nueva aplicación y una página con un mapa. A continuación, inspeccione la página resultante para conocer la región de mapa.

Tiempo de laboratorio estimado: 10 minutos

### Objetivos

*   Descripción de los conceptos básicos de la región de mapa de APEX

### Requisitos

*   Laboratorio 1: Instalación de la aplicación de mapas de muestra

## Tarea 1: Creación de una Nueva Aplicación con una Página de Mapa con el Asistente

El asistente proporciona una forma rápida y sencilla de crear una nueva aplicación y su primer mapa.

1.  Vaya a **Creador de aplicaciones** y haga clic en **Crear**. ![Asistente de creación de aplicaciones en App Builder](images/create-map-01.png)
    
2.  Seleccione **Nueva aplicación**. ![Crear una aplicación - Nueva aplicación](images/create-map-02.png)
    
3.  Introduzca un nombre para la aplicación y haga clic en **Agregar página**. ![Crear una solicitud - Formulario](images/create-map-03.png)
    
4.  Seleccione **Asignación** como tipo de página. ![Crear una aplicación: agregar página](images/create-map-04.png)
    
    **Nota:** Este asistente es el mismo que el uso de **Crear Página** en una aplicación existente.
    
5.  Introduzca **Asignación de Aeropuertos** como Nombre de Página. (Con este asistente, el Nombre de Página también se utilizará como nombre de la Región de Asignación creada en la página). Haga clic en el icono situado a la derecha de la entrada de la tabla para seleccionar la tabla **EBA\_SAMPLE\_MAP\_AIRPORTS**. Para la columna de geometría, seleccione **GEOMETRY** y, por último, seleccione una columna para utilizar una pista al pasar el mouse sobre un elemento del mapa. ![Creación de una Aplicación: Página Crear Mapa](images/create-map-05.png)
    
6.  Observe que la nueva página aparece ahora en **Páginas**. Haga clic en **Crear aplicación**. ![Crear una aplicación: finalizar la creación de la aplicación](images/create-map-06.png)
    
7.  Se le dirigirá a la página en la que gestionará la nueva aplicación. Haga clic en **Ejecutar aplicación**. ![Ejecutar aplicación](images/create-map-07.png)
    
8.  Conéctese a su aplicación con su nombre de usuario y contraseña de conexión a APEX. ![Iniciar sesión en la aplicación](images/create-map-08.png)
    
9.  El diseño predeterminado que hemos seleccionado para nuestra aplicación proporciona una página de inicio con enlaces a otras páginas. En la página de inicio, navegue hasta la página que acaba de crear. ![Página Inicio de Aplicación](images/create-map-09.png)
    
10.  Observe que la página incluye un mapa interactivo que muestra las ubicaciones de los aeropuertos con información sobre herramientas según lo configurado. ![Ver el mapa](images/create-map-10.png)
    

## Tarea 2: Inspeccionar la página de mapa

Ahora inspeccionará la región de mapa creada por el asistente.

1.  En la barra de herramientas del desarrollador situada en la parte inferior de la página, haga clic en el botón **Página 2** para editar la página. ![Editar la página](images/create-map-11.png)
    
2.  En el árbol Página de la izquierda, en **Cuerpo**, haga clic en **Mapa de aeropuertos**. Este es el título de la región de mapa creada por el asistente de creación de páginas. Es, por defecto, el mismo que el título de la página y se puede cambiar según lo desee. En el panel Detalles de región de la derecha, observe que esta región tiene el tipo **Mapa**. ![Ver propiedades de la página](images/create-map-12.png)
    
3.  Las regiones de mapa incluyen capas que son los puntos, líneas y polígonos (de Oracle Spatial, GeoJSON o coordenadas) que se muestran en la parte superior de un mapa de fondo. Al desplazarse por el asistente Crear Página, ha seleccionado una asignación mediante la columna GEOMETRY de la tabla EBA\_SAMPLE\_MAP\_AIRPORTS (es decir, datos de Oracle Spatial). Así que el asistente ha creado una capa que contiene las ubicaciones del aeropuerto. Por defecto, la capa tiene el mismo nombre que la página, es decir, **mapa de aeropuertos**. Esto se puede cambiar según se desee.
    
    Para inspeccionar esta capa, en el árbol Página del panel izquierdo, en Capas, haga clic en **Mapa de aeropuertos**. Los detalles de configuración se muestran en el panel **Capa** de la derecha. Para obtener información sobre los elementos de configuración, haga clic en el separador **Ayuda** del panel central. Al hacer clic en los elementos de configuración, se muestra información de ayuda para ese elemento. Por ejemplo, haga clic en el menú **Tipo de capa** para ver la ayuda sobre sus opciones. ![Inspeccionar propiedades de capa de mapa](images/create-map-13.png)
    
4.  Desplácese hacia abajo en el panel Capa para ver las otras opciones de configuración definidas por el asistente, incluida la asignación de columnas, donde se define el tipo de datos de geometría. Aquí está utilizando el tipo de dato espacial nativo de Oracle, SDO\_GEOMETRY, y el nombre de columna es GEOMETRY. ![Inspeccionar propiedades de capa de mapa](images/create-map-14.png)
    

Felicidades por crear tus primeros mapas. Hay mucha capacidad más allá de lo básico que acaba de explorar. No dude en experimentar con ajustes en los parámetros y, a continuación, guardar y ejecutar para ver los resultados. En el siguiente laboratorio, configurará una nueva región de mapa desde cero.

Esto concluye el laboratorio. Ahora puede pasar a la siguiente práctica de laboratorio.

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, Database Product Management, marzo de 2023