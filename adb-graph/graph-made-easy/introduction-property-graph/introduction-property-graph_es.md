# Trabajar con Graph Studio

## Acerca de este taller

En este taller se presentan conceptos clave de análisis y modelado de datos de gráficos mediante las funciones de Graph Studio de una instancia de Autonomous Database. Muestra cómo usar consultas de gráficos para buscar pagos circulares que puedan indicar transacciones fraudulentas, y algoritmos de análisis de gráficos para identificar cuentas a través de las cuales fluyen muchas transacciones. Consultará datos que contengan información (artificial) de cuentas y transacciones. Comenzará por crear un gráfico, consultar el gráfico, ejecutar un algoritmo de análisis y visualizar los resultados. Una sección opcional introduce conceptos de gráficos semánticos (RDF), que se suelen utilizar para los gráficos de conocimientos, y muestra cómo cargar datos de un formato de gráfico RDF estándar, como el formato n-triple, y cómo consultarlos mediante SPARQL, el lenguaje de consulta para los gráficos RDF.

Tiempo estimado del taller: 75 minutos

Si desea ver cómo hacemos el taller, haga clic [aquí](https://youtu.be/Ymk9TE9Q2K4).

### Acerca de Graph Studio

Oracle Autonomous Database tiene funciones que le permiten funcionar como una base de datos de gráficos escalable. Automatizan la creación de modelos de gráficos y gráficos en memoria a partir de tablas de base de datos. Incluyen blocs de notas y API de desarrollador para ejecutar consultas de gráficos mediante PGQL, un lenguaje de consulta de gráficos similar a SQL, más de 60 algoritmos de gráficos incorporados que utilizan API de Java o Python y visualización de gráficos nativa.

Vea los siguientes dos vídeos para obtener más información sobre Graph Studio. La primera es una introducción a los gráficos de propiedades y sus casos de uso. El segundo es un recorrido por la interfaz de Graph Studio.

[Simplifique los análisis de gráficos con Autonomous Database](youtube:eCd-969hrak) Simplifique los análisis de gráficos con Autonomous Database

[Autonomous Database: un recorrido por la interfaz de Graph Studio](youtube:S6Q-IJcBkU0) Autonomous Database: un recorrido por la interfaz de Graph Studio

### Objetivos

En este taller:

*   Crear un gráfico mediante la sentencia CREATE PROPERTY GRAPH de PGQL (un lenguaje de consulta de gráficos)
*   Cargar el grafo en la memoria para su análisis
*   Crear un Notebook
*   Consultar y visualizar el gráfico mediante párrafos de bloc de notas PGQL
*   Ejecutar algoritmos de gráficos y visualizar los resultados

### Requisitos

*   Cuenta de Oracle Cloud
*   Instancia sin servidor de Autonomous Database aprovisionada

Esto concluye este laboratorio. **Ahora puede continuar con la siguiente práctica de laboratorio.**

## Reconocimientos

*   **Autor**: Jayant Sharma, gestión de productos
*   **Contribuyentes**: Jayant Sharma, gestión de productos
*   **Última actualización por/fecha**: Ramu Murakami Gutiérrez, mánager de productos, agosto de 2023