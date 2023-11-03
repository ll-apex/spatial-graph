# Introducción

## Acerca de Oracle Spatial

La misión de Oracle es ayudar a las personas a ver los datos de nuevas formas, descubrir información y desbloquear infinitas posibilidades. El análisis espacial consiste en comprender interacciones complejas basadas en relaciones geográficas: responder preguntas basadas en la ubicación de las personas, los activos y los recursos. Las estadísticas espaciales permiten proporcionar un mejor servicio al cliente, optimizar el personal, localizar centros minoristas y de distribución, evaluar campañas de ventas y marketing, etc. Con las ofertas espaciales de Oracle, los desarrolladores, profesionales de bases de datos y analistas pueden utilizar un conjunto completo de herramientas de visualización, análisis y gestión de datos espaciales para integrar el análisis espacial y la asignación en aplicaciones en una infraestructura de gestión de datos empresarial: Oracle Database y Oracle Exadata. Las aplicaciones espaciales disponen de tecnologías innovadoras de Oracle Cloud y Oracle Autonomous Database, la única base de datos del sector con autogestión, autoseguridad y autorreparación.

Como se muestra a continuación, las funciones espaciales de Oracle Database proporcionan almacenamiento, procesamiento y análisis escalables y eficaces de tipos de datos espaciales básicos y avanzados. También se proporciona una serie de componentes Java EE desplegables para soportar servicios comunes de nivel medio.

![texto alt img](./images/spatial-platform.png)

Para obtener más información, visite \[https://oracle.com/goto/spatial\] (https://oracle.com/goto/spatial)

Tiempo de taller estimado: 60 minutos

### Resumen del taller

En este taller, creará, configurará y analizará datos espaciales. Creará y configurará tablas espaciales para STORES, WAREHOUSES, REGIONS y TORNADO\_PATHS a partir de formatos comunes y, a continuación, realizará consultas espaciales para explorar sus relaciones en función de la proximidad y la contención. Finalmente, puede transformar los resultados mediante el soporte JSON nativo en ADB, para la integración de desarrolladores.

La capacidad de relacionar información basada en la ubicación, como relacionar datos basados en la proximidad espacial y la contención, es extremadamente valiosa en innumerables escenarios. No hay ninguna clave preexistente que relacione las ubicaciones de tienda con un almacén. Pero Spatial permite determinar tal relación en función de la proximidad. Del mismo modo, no existe ninguna relación preexistente entre las ubicaciones de tiendas y las regiones, por ejemplo, las regiones fiscales. Pero el espacio permite que su relación se determine en función de la contención. Más allá, Spatial permite el análisis basado en la ubicación, como resumir la información basada en la proximidad; por ejemplo, la pérdida debido a tornados a una distancia de una ubicación. En lugar de realizar estos análisis en un sistema independiente, puede aprovechar las funciones espaciales incorporadas de ADB.

Obtendrá experiencia con todas las capacidades mencionadas anteriormente en este taller.

### Requisitos

\- Cuenta de Oracle Cloud : este taller requiere acceso a un cliente SQL y de Oracle Database (es decir, SQL Developer, SQL Developer Web, SQL\*Plus). Si ya tiene acceso a ellos, después de esta introducción puede acceder a la sección Crear datos de ejemplo. De lo contrario, debe continuar con las secciones Cuenta de Oracle Cloud, Autonomous Database y SQL Developer Web. - No se necesita experiencia previa con Oracle Spatial. - Cuenta de Oracle Cloud

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Contribuyentes**: Karin Patenge, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, septiembre de 2022