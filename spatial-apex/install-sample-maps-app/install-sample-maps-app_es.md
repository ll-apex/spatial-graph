# Instalación de la Aplicación de Mapas de Ejemplo

## Introducción

Oracle APEX proporciona acceso a una cartera de aplicaciones de ejemplo que resaltan áreas específicas de funcionalidad. Entre ellas se encuentra la aplicación Sample Maps, que muestra las capacidades de asignación en Oracle APEX. Se proporciona una amplia variedad de ejemplos para servir como ejemplos funcionales y puntos de partida para una mayor personalización. En este laboratorio, instalará y configurará la aplicación Sample Maps.

Tiempo de laboratorio estimado: 15 minutos

### Objetivos

*   Instalar la aplicación de mapas de muestra
*   Cargar datos de apoyo

### Requisitos

*   Se necesita Oracle APEX 21.1+. Las capturas de pantalla de este taller se realizan con APEX 21.2. Dado que generalmente recomendamos utilizar la [última versión de APEX](https://www.oracle.com/tools/downloads/apex-downloads/), se esperan pequeñas diferencias ocasionales en la interfaz de usuario.

## Tarea 1: Instalación de la aplicación

1.  Comience haciendo clic en **Creador de aplicaciones**.
    
    ![Application Builder de APEX](images/install-sample-maps-00.png)
    
2.  Haga clic en **Install a Starter or Sample App**.
    
    ![Seleccionar aplicación inicial o de ejemplo](images/install-sample-maps-01.png)
    
    **Nota:** Si el espacio de trabajo tiene aplicaciones existentes, haga clic en **Crear** y, a continuación, en **Aplicación de inicio**.
    
3.  Haga clic en **Muestras** para abrir un nuevo separador del explorador con una lista de aplicaciones de ejemplo disponibles.
    
    ![Seleccionar muestras](images/install-sample-maps-02.png)
    
4.  Desplácese hacia abajo hasta **Asignaciones de ejemplo** y haga clic en **Descargar aplicación**.
    
    ![Texto alternativo de imagen](images/install-sample-maps-03.png)
    
    Se le pedirá que guarde el paquete de aplicaciones en una carpeta local.
    
    **Nota:** Si se le redirige a github, vaya a la carpeta de la versión de APEX y descargue **sample-maps.zip**.
    
5.  Vuelva al separador del explorador del creador de aplicaciones y haga clic en **Importar**.
    
    ![Seleccionar importación](images/install-sample-maps-04.png)
    
6.  Arrastre y suelte o busque el archivo zip de la aplicación Sample Maps que ha descargado anteriormente. Deje la selección File Type como Database Application y, a continuación, haga clic en **Next** (Siguiente).
    
    ![Seleccionar zip de aplicación de mapas de ejemplo](images/install-sample-maps-05.png)
    
7.  Se confirmó la importación del archivo. Haga clic de nuevo en **Siguiente**.
    
    ![Haga clic en Next.](images/install-sample-maps-06.png)
    
8.  Deje las selecciones del menú por defecto y haga clic en **Install Application** (Instalar aplicación).
    
    ![Haga clic en Install Application.](images/install-sample-maps-07.png)
    
    Accederá al asistente Install Application.
    
9.  Deje las selecciones de menú por defecto y haga clic en **Next** (Siguiente).
    
    ![Haga clic en Next.](images/install-sample-maps-08.png)
    
10.  Haga clic en **Siguiente** para validar la compatibilidad del sistema.
    

![Haga clic en Next.](images/install-sample-maps-09.png)

11.  Con la compatibilidad confirmada, haga clic en **Instalar** para iniciar la instalación de objetos de base de datos de soporte y la aplicación APEX.

![Haga clic en Instalar](images/install-sample-maps-10.png)

12.  Una vez finalizada la instalación, haga clic en **Ejecutar aplicación**.

![Haga clic en Ejecutar Aplicación](images/install-sample-maps-11.png)

13.  Conéctese a la aplicación Sample Maps con el nombre de usuario y la contraseña del espacio de trabajo de APEX.

![Conectar](images/install-sample-maps-12.png)

## Tarea 2: Carga de datos

1.  Ahora se encuentra en la aplicación Sample Maps, que proporciona numerosos ejemplos de mapas y operaciones espaciales en APEX. En el inicio inicial se muestra un mensaje de advertencia sobre la carga de datos. Haga clic en el enlace **Carga de datos** de ese mensaje. Accederá a una página en la que completará la carga de datos de demostración.
    
    ![Haga clic en Data Loading](images/install-sample-maps-13.png)
    
2.  La página Carga de datos muestra el estado de carga de los conjuntos de datos de estados y aeropuertos utilizados por la aplicación Mapas de ejemplo y el resto de este taller. Tras la instalación de la aplicación Mapas de ejemplo, estos conjuntos de datos solo se cargan parcialmente. Para completar la carga de datos de ejemplo, puede cargar directamente desde archivos almacenados en github o puede descargar primero los archivos y cargarlos desde su sistema local. Si ejecuta APEX en una red que necesita un proxy para acceder a github, debe utilizar la última opción.
    
    Si la instancia de APEX no necesita un proxy para acceder a github (por ejemplo, apex.oracle.com o APEX con Oracle Autonomous Database), haga clic en el botón para cargar **directamente desde GitHub** y, a continuación, haga clic en **Cargar juego de datos** en la parte superior derecha.
    
    ![Haga clic directamente desde Github](images/install-sample-maps-14.png)
    
    Si la instancia de APEX necesita un proxy para acceder a github (por ejemplo, APEX que se ejecuta detrás del firewall corporativo) o si tiene otros problemas al cargar directamente desde github, haga clic en el botón **Cargar archivos**, que proporciona instrucciones alternativas.
    
3.  Cuando se complete la carga de datos, verá una notificación en la parte superior derecha y el mensaje de advertencia desaparecerá. La aplicación Mapas de ejemplo ya está lista para su uso.
    
    ![Confirmación de carga de datos](images/install-sample-maps-15.png)
    

## Tarea 3: Exploración de la aplicación de mapas de ejemplo

1.  Al hacer clic en cualquiera de los mosaicos, se accede a la página asociada de la aplicación. Por ejemplo, haga clic en **Asignar e informar**.
    
    ![Vaya a la página Map and Report.](images/install-sample-maps-16.png)
    
2.  En esta página, hacer clic en un elemento del informe de la derecha se centra en el elemento del mapa y abre una ventana de información. Al hacer clic en el icono de la esquina superior izquierda, se abre un panel de navegación para acceder a otras páginas de la aplicación.
    
    ![Interactuar con el mapa](images/install-sample-maps-17.png)
    
3.  Haga clic en los elementos del panel de navegación para acceder a otras páginas de la aplicación.
    
    ![El panel de navegación muestra otras páginas](images/install-sample-maps-18.png)
    
4.  Para cerrar el panel de navegación, haga clic en el icono situado en la parte superior izquierda. También puede navegar a la página de inicio de la aplicación haciendo clic en **Asignaciones de ejemplo** en la parte superior izquierda.
    
    ![Cerrar panel de navegación](images/install-sample-maps-19.png)
    

## Tarea 4: Exploración de los datos de demostración

1.  Vuelva a APEX, haga clic en **Taller de SQL** y, a continuación, en **Explorador de objetos**.
    
    ![Taller de SQL - Explorador de objetos](images/install-sample-maps-20.png)
    
2.  Observe las tablas creadas por el paso de carga de datos realizado anteriormente. Haga clic en **EBA\_SAMPLE\_MAP\_AIRPORTS**. Observe que las columnas incluyen una columna denominada GEOMETRY que tiene el tipo SDO\_GEOMETRY (tipo de dato espacial nativo de Oracle).
    
    ![Tabla con columna de geometría nativa](images/install-sample-maps-21.png)
    
3.  Haga clic en la pestaña **Datos** para ver el contenido de la tabla.
    
    ![Contenido de la tabla](images/install-sample-maps-22.png)
    
    A continuación, desplácese a la derecha para ver la columna de geometría. Puesto que los aeropuertos se almacenan como puntos, APEX muestra una representación de cadena del valor de geometría de puntos. Los puntos siempre se basan en una sola coordenada, por lo que tiene sentido que APEX muestre el valor de esta forma.
    
    ![geometrías de puntos](images/install-sample-maps-23.png)
    
4.  Haga clic en **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES**. De nuevo, observe que las columnas incluyen una columna denominada GEOMETRY que tiene el tipo SDO\_GEOMETRY (tipo de dato espacial nativo de Oracle).
    
    ![Tabla con columna de geometría nativa](images/install-sample-maps-24.png)
    
5.  Haga clic en el separador **Datos** para ver el contenido de la tabla. Dado que esta tabla almacena estados, las geometrías son polígonos. APEX no muestra una representación de cadena de estos valores, ya que pueden incluir juegos de coordenadas extremadamente largos.
    
    ![geometrías de polígonos](images/install-sample-maps-25.png)
    
6.  Observe las tablas con nombres como **MDRT\_....$**. La base de datos crea y gestiona automáticamente estos índices en segundo plano para soportar índices espaciales en otras tablas. Estas tablas nunca se crean, actualizan ni suprimen manualmente. Son únicamente para apoyar operaciones de análisis espacial y pueden ser ignorados.
    
    ![Artefactos de índice espacial](images/install-sample-maps-26.png)
    
7.  Por último, puede ejecutar una consulta espacial básica con estos datos. Haga clic en **Taller SQL** y, a continuación, en **Comandos SQL**.
    
    ![SQL Workshop - Comandos SQL](images/install-sample-maps-27.png)
    
8.  La siguiente consulta devuelve el número de aeropuertos con cobertura de tierra de más de 1000 acres que se encuentran a 100 km de Texas. Observe el uso del operador espacial nativo **sdo\_within\_distance**. Copie y pegue la consulta en la ventana Comandos SQL y, a continuación, haga clic en **Ejecutar** en la parte superior derecha.
    
        <copy>
        select count(a.id) as number_of_airports
        from EBA_SAMPLE_MAP_AIRPORTS a,
              EBA_SAMPLE_MAP_SIMPLE_STATES b
        where b.state_code= 'TX'
           and land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance=100 unit=KM') = 'TRUE'
        </copy>
        
    
    ![Consulta espacial](images/install-sample-maps-28.png)
    
9.  En el operador sdo\_within\_distance, actualice la distancia a 300 km y vuelva a ejecutarlo. Observe los cambios de resultados según el área de búsqueda más grande.
    
    ![Consulta espacial](images/install-sample-maps-29.png)
    

En una práctica posterior, configurará un mapa que muestre los resultados de esta consulta donde el estado y la distancia estén controlados por los menús de la página.

Ahora ha instalado y explorado la aplicación y los datos de Mapas de ejemplo. A continuación, pasa a crear tu propia aplicación y mapas.

Esto concluye el laboratorio. Ahora puede pasar a la siguiente práctica de laboratorio.

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Contribuyentes**: Carsten Czarski, Desarrollo de APEX, Oracle
*   **Última actualización por/fecha**: David Lapp, Database Product Management, marzo de 2023