# Crear un grafo RDF en Graph Studio

## Introducción

Graph Studio de Oracle Autonomous Database permite a los usuarios modelar, crear, consultar y analizar datos de gráficos. Incluye blocs de notas, API de desarrollador para ejecutar consultas de gráficos mediante PGQL, más de 60 algoritmos de gráficos incorporados y ofrece docenas de visualizaciones, incluida la visualización de gráficos nativa. Además del gráfico de propiedades, Graph Studio ahora amplía el soporte para tecnologías semánticas, incluidas las capacidades de almacenamiento, inferencia y consulta de datos y ontologías basadas en Resource Description Framework (RDF) y Web Ontology Language (OWL). Ahora puede usar Graph Studio para las siguientes funciones de RDF admitidas:

*   Crear un grafo RDF
*   Ejecutar consultas SPARQL en el gráfico RDF de un párrafo de bloc de notas
*   Analizar y visualizar gráficos de RDF

Tiempo estimado: 5 minutos

Vea el siguiente vídeo para una breve introducción al laboratorio. [Creación de un gráfico de RDF en Graph Studio](videohub:1_vvqhh26v)

### Objetivos

*   Crear grafo RDF en Graph Studio
*   Validar el gráfico RDF
*   Ejecutar consultas SPARQL en la página Playground

### Requisitos

*   El siguiente ejercicio práctico requiere una instancia de Autonomous Database: sin servidor.
*   Y que existe el usuario activado para gráficos (GRAPHUSER). Es decir, existe un usuario de base de datos con los roles y privilegios correctos.

## Tarea 1: Creación de un grafo RDF en Graph Studio

Suponiendo que ha completado las prácticas anteriores y que está conectado actualmente, ejecute los siguientes pasos:

1.  Haga clic en **Gráficos** en el menú de navegación de la izquierda para navegar por la página Gráficos.

![La página de llegada después de crear el entorno es el menú Jobs.](./images/graph-studio-home.png)

2.  En el menú desplegable Tipo de gráfico, seleccione **RDF** y, a continuación, haga clic en el botón **Crear** en la esquina superior derecha de la interfaz.

![El menú desplegable de tipo de gráfico de la página Graph Studio muestra las opciones de gráfico PG y RDF](./images/graph-studio-graphs.png)

3.  Seleccione **Gráfico RDF** y, a continuación, haga clic en el botón **Confirmar**.

![botón de confirmación para seleccionar la opción de gráfico rdf](./images/click-confirm-rdf.png)

4.  El Asistente de Creación de Gráficos de RDF se abre como se muestra:

![La página Crear gráfico RDF.](./images/create-rdf-graph.png)

5.  Introduzca la ruta de URI de OCI Object Storage:
    
          <copy>https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt
        
6.  Haga clic en **No hay credenciales**.
    
7.  Haga clic en **Siguiente**. Debe aparecer el siguiente cuadro de diálogo, introduzca "MOVIESTREAM" para Graph Name:
    

![La segunda página 'crear gráfico de RDF'](./images/create-rdf-graph-2.png)

8.  Haga clic en **Crear**.
    
    Se iniciará el trabajo de creación de gráficos de RDF. Dado que el archivo RDF contiene 139461 registros, el proceso puede tardar entre 3 y 4 minutos. Puede supervisar el trabajo en la página **Trabajos** de Graph Studio.
    

![La página 'jobs' de Graph Studio muestra un trabajo 'Create a RDF Graph - MOVIESTREAM' aún en curso](./images/graph-studio-jobs.png)

    When succeeded, the status will change from pending to succeeded and Logs can be viewed by clicking on the three dots on the right side of the job row and selecting **See Log**. The log for the job displays details as shown below:
    
    ```
    Tue, Mar 1, 2022 08:21:04 AM
    Finished execution of task Graph Creation - MOVIESTREAM.
    
    Tue, Mar 1, 2022 08:21:04 AM
    Graph MOVIESTREAM created successfully
    
    Tue, Mar 1, 2022 08:21:04 AM
    Optimizer Statistics Gathered successfully
    
    Tue, Mar 1, 2022 08:20:50 AM
    External table <graph-user>_TAB_EXTERNAL dropped successfully
    
    Tue, Mar 1, 2022 08:20:49 AM
    Data successfully bulk loaded from ORACLE_ORARDF_STGTAB
    
    Tue, Mar 1, 2022 08:20:39 AM
    Model MOVIESTREAM created successfully
    
    Tue, Mar 1, 2022 08:20:37 AM
    Network RDF_NETWORK created successfully
    
    Tue, Mar 1, 2022 08:20:24 AM
    Data loaded into the staging table ORACLE_ORARDF_STGTAB from <graph-user>_TAB_EXTERNAL
    
    Tue, Mar 1, 2022 08:20:19 AM
    External table <graph-user>_TAB_EXTERNAL created successfully
    
    Tue, Mar 1, 2022 08:20:19 AM
    Using the Credential MOVIES_CREDENTIALS
    
    Tue, Mar 1, 2022 08:20:19 AM
    Started execution of task Graph Creation - MOVIESTREAM.
    ```
    

## Tarea 2: Validar el gráfico RDF

Puede explorar y validar el gráfico de RDF recién creado en la página **Gráficos** de Graph Studio, como se muestra a continuación:

1.  Navegue a la página **Gráficos** y defina el **tipo de gráfico** en RDF mediante el menú desplegable. Seleccione la fila del gráfico MOVIESTREAM de los gráficos RDF disponibles, las sentencias de ejemplo (deben aparecer triples o cuádruples), utilice los tres puntos horizontales para cambiar el tamaño de estas sentencias y ponerlas a la vista. En el panel inferior, como se muestra, se muestran ejemplos de sentencias (triples o cuadrículas) del gráfico RDF:

![Las sentencias de ejemplo del gráfico RDF 'MOVIESTREAM' se muestran en trillizos](./images/graph-sample-statements.png)

2.  Después de seleccionar el gráfico MOVIESTREAM, desplácese hasta la parte inferior de la página y verifique que se han recuperado 500 filas de triples RDF.

![Ejemplos de sentencias del gráfico RDF MOVIESTREAM](./images/sample-statements.png)

## Tarea 3: Ejecutar consultas SPARQL en la página del patio de recreo

Puede ejecutar consultas SPARQL en el gráfico RDF desde la página **Query Playground**.

1.  En la página **Gráficos**, seleccione **RDF** en el menú desplegable Tipo de Gráfico y haga clic en el botón **Consulta** para navegar a la página Área de Reproducción de Consulta.

![Página de gráficos con el tipo de gráfico RDF seleccionado y el botón de consulta resaltado](./images/graph-type.png)

2.  Si tiene varios gráficos en Graph Studio, tendrá que elegir el gráfico que desea consultar. En el menú Graph Name, seleccione MOVIESTREAM en el menú desplegable.

![El campo de juego de consultas muestra el nombre del gráfico 'MOVIESTREAM' seleccionado en el menú desplegable](./images/query-playground.png)

3.  Ejecute la siguiente consulta para el gráfico de RDF.
    
        <copy>PREFIX rdf: &lthttp://www.w3.org/1999/02/22-rdf-syntax-ns#&gt
        PREFIX rdfs: &lthttp://www.w3.org/2000/01/rdf-schema#&gt
        PREFIX xsd: &lthttp://www.w3.org/2001/XMLSchema#&gt
        PREFIX ms: &lthttp://www.example.com/moviestream/&gt
        
        SELECT DISTINCT ?gname
        WHERE {
          ?movie ms:actor/ms:name "Keanu Reeves" ;
          ms:genre/ms:genreName ?gname .
        }
        ORDER BY ASC(?gname)<copy>
        
    
    Cuando la consulta se ejecuta correctamente, la salida de la consulta se mostrará como se muestra:
    

![El campo de juego de consultas muestra la ejecución correcta de una consulta en el gráfico RDF MOVIESTREAM y muestra los resultados de la consulta](./images/query-playground-script.png)

Esto concluye este laboratorio. **Ahora puede continuar con la siguiente práctica de laboratorio.**

## Reconocimientos

*   **Autor**: Malia German, Ethan Shmargad, Matthew McDaniel Solution Engineers, Ramu Murakami Gutiérrez Product Manager
*   **Colaborador técnico**: Melliyal Annamalai Distinguished Product Manager, Joao Paiva Consulting Miembro del personal técnico, Lavanya Jayapalan Principal User Assistance Developer
*   **Última actualización por/fecha**: Ramu Murakami Gutiérrez, mánager de productos, agosto de 2023