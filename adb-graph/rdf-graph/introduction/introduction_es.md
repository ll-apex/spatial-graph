# Trabajo con gráficos RDF en Graph Studio

## Introducción

Graph Studio de Oracle Autonomous Database permite a los usuarios modelar, crear, consultar y analizar datos de gráficos. Incluye blocs de notas, API de desarrollador para ejecutar consultas de gráficos mediante PGQL, más de 60 algoritmos de gráficos incorporados y ofrece docenas de visualizaciones, incluida la visualización de gráficos nativa. Además del gráfico de propiedades, Graph Studio ahora amplía el soporte para tecnologías semánticas, incluidas las capacidades de almacenamiento, inferencia y consulta de datos y ontologías basadas en Resource Description Framework (RDF) y Web Ontology Language (OWL). Ahora puede usar Graph Studio para las siguientes funciones de RDF admitidas:

*   Crear un grafo RDF
*   Ejecutar consultas SPARQL en el gráfico RDF de un párrafo de bloc de notas
*   Analizar y visualizar gráficos de RDF

RDF es un modelo de datos estándar W3C para representar datos enlazados. RDF utiliza identificadores uniformes de recursos (URI) como identificadores únicos globales para recursos y URI para asignar un nombre a la relación entre dos recursos. Además de los URI, RDF utiliza literales para representar valores escalares como números, cadenas y registros de hora. Los modelos RDF vincularon los datos como un gráfico dirigido y etiquetado, donde cada borde generalmente se denomina triple. El vértice fuente del borde se llama el sujeto del triple. La etiqueta o el nombre del borde se denomina predicado del triple y el vértice de destino del borde se denomina objeto del triple. Los gráficos RDF son particularmente adecuados para los gráficos de conocimiento y las aplicaciones de integración de datos porque los URI proporcionan identificadores únicos a nivel mundial y la estructura triple simple y sin esquema hace que sea muy fácil combinar datos de varios gráficos RDF diferentes en un solo gráfico. Además, RDFS y OWL proporcionan formas estándar de definir vocabularios reutilizables (juegos de etiquetas de borde semánticamente significativas y tipos de recursos) para datos de gráficos más interoperables y procesables por máquina. Consulte [aquí](https://www.w3.org/TR/rdf11-primer/) para obtener más información sobre los estándares W3C RDF 1.1.

El protocolo SPARQL y el lenguaje de consulta RDF (SPARQL) son una de las tecnologías estandarizadas por W3C para consultar datos de Resource Description Framework (RDF). Puede obtener más información sobre el estándar W3C SPARQL 1.1 [aquí](https://www.w3.org/TR/sparql11-overview/).

SPARQL utiliza una estructura **SELECCIONAR Algunos Elementos WHERE Some Conditions** para especificar una consulta. Las condiciones de la cláusula WHERE de una consulta SPARQL se crean mediante patrones triples, que son esencialmente un triple de RDF donde los elementos del triple se pueden sustituir por variables de consulta (con un prefijo ?). Una variable de consulta en un patrón triple actúa como comodín. Considere el patrón triple **?movie ms:genre ms:genre\_Comedy**. Cuando este patrón triple se evalúa frente a un gráfico RDF, devolverá todos los **sujetos** de triples con el predicado **ms:genre** y **object ms:genre\_Comedy**. La cláusula SPARQL SELECT especifica una lista de variables de consulta para proyectar desde la consulta. En la sintaxis SPARQL, los URI están entre corchetes angulares y los literales entre comillas dobles (por ejemplo, "Kevin Bacon"). Los literales pueden ir seguidos de ^^ y un URI de tipo de dato (por ejemplo, "100"^^[http://www.w3.org/2001/XMLSchema#integer](http://www.w3.org/2001/XMLSchema#integer)) o seguido de @ y una etiqueta de idioma (por ejemplo, "Jalapeño"@es). La mayoría de los tipos de dato de esquema XML están soportados en SPARQL, y se considera que los literales sin formato sin URI de tipo de dato tienen el tipo de dato [http://www.w3.org/2001/XMLSchema#string](http://www.w3.org/2001/XMLSchema#string).

Este vídeo que se muestra a continuación es un ejemplo de demostración con un conjunto de datos similar que se utilizará en esta práctica. Este video enfatiza la estructura de la ontología de la estructura de la película usando RDF. La demostración presenta RDF Graph utilizando una tabla temporal en combinación con SQL Developer, que es claramente diferente de esta versión de Autonomous Database del laboratorio. Sin embargo, el lenguaje SPARQL utilizado para consultar y visualizar los datos es muy similar para el contexto.

[](youtube:e_EQjInas50)

En este laboratorio, se creará un gráfico semántico utilizando SPARQL, que es una metodología estandarizada para integrar diferentes orígenes de datos. Este procedimiento le enseñará a analizar los datos mediante consultas y visualización basadas en gráficos.

Tiempo estimado: 35 minutos

### Objetivos

*   Preparar el Entorno
*   Introducción a los gráficos RDF
*   Creación y validación de un usuario de gráfico RDF en Graph Studio
*   Consulta y Visualización del Gráfico de RDF

### Requisitos

En este laboratorio se asume que tiene:

*   Una cuenta de Oracle Cloud: consulte la página de llegada LiveLabs de este taller para ver qué entornos están soportados

*   Descargue el archivo MOVIESTREAM (moviestream\_rdf.nt) mediante este [enlace](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)

Esto concluye este laboratorio. Ahora puede _proceder al siguiente laboratorio._

## Reconocimientos

*   **Autor**: Nicholas Cusato, Ethan Shmargad, Matthew McDaniel Solution Engineers, Ramu Murakami Gutiérrez, director de productos
*   **Colaborador técnico**: Melliyal Annamalai Distinguished Product Manager, Joao Paiva Consulting Miembro del personal técnico, Lavanya Jayapalan Principal User Assistance Developer
*   **Última actualización por/fecha**: mánager de productos de Ramu Murakami Gutiérrez, junio de 2023