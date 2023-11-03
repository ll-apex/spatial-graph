# Uso de Graph Analytics para recomendar películas

## Introducción

En este taller, utilizará Graph Studio para detectar y crear comunidades de clientes en función del comportamiento de visualización de películas. Una vez que hayas creado comunidades, haz recomendaciones basadas en lo que los miembros de tu comunidad han visto.

Tiempo estimado: 60 minutos

### Acerca de Graph Studio

Oracle Autonomous Database tiene funciones que le permiten funcionar como una base de datos de gráficos de propiedades escalable. Automatizan la creación de modelos de gráficos y gráficos en memoria a partir de tablas de base de datos. Incluyen blocs de notas y API de desarrollador para ejecutar consultas de gráficos mediante PGQL, un lenguaje de consulta de gráficos similar a SQL y más de 60 algoritmos de gráficos incorporados, así como muchas visualizaciones, incluida la visualización de gráficos nativa.

Vea el siguiente vídeo que ofrece una introducción a los gráficos de propiedades y sus casos de uso.

Simplifique los análisis de gráficos con Autonomous Database

[](youtube:eCd-969hrak)

En este taller utilizará un gráfico creado a partir de las tablas MOVIE, CUSTOMER\_PROMOTIONS y CUSTSALES\_PROMOTIONS. MOVIE y CUSTOMER\_PROMOTIONS son tablas de vértice (cada fila de estas tablas se convierte en un vértice). CUSTSALES\_PROMOTIONS conecta las dos tablas y es la tabla perimetral. Cada vez que un cliente de CUSTOMER\_PROMOTIONS alquila una película en la tabla MOVIE, eso es una ventaja en el gráfico. Este gráfico se ha creado para su uso en este taller.

Puede elegir entre más de 60 algoritmos incorporados al analizar un gráfico. En este taller, utilizará el algoritmo **SALSA personalizado**, que es una buena opción para las recomendaciones de productos. Los vértices de cliente se asignan a _hubs_ y las películas a _autoridades_. Las puntuaciones de hub más altas indican una relación más estrecha entre los clientes. Las puntuaciones de autoridad más altas indican que el vértice (o película) juega un papel más importante en el establecimiento de esa cercanía.

### Objetivos

En este taller, utilizará la función Graph Studio de Autonomous Database para:

*   Utilizar un cuaderno de notas
*   Ejecutar algunas consultas de gráficos PGQL
*   Utilizar python para ejecutar SALSA personalizado desde la biblioteca de algoritmos
*   Consultar y guardar las recomendaciones

### Requisitos

*   Cuenta de Oracle Cloud

## Reconocimientos

*   **Autor**: Melli Annamalai, mánager de productos, Oracle Spatial and Graph
*   **Contribuyentes**: Jayant Sharma
*   **Última actualización por/fecha**: Ramu Murakami Gutiérrez, mánager de productos de Oracle Spatial and Graph, febrero de 2023.