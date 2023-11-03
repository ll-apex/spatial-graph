# Introducción

## Acerca de este taller

En este taller explorará la asignación en Oracle APEX mediante la función Map Region y Oracle Spatial. Instalará y explorará una aplicación de ejemplo incorporada con muchos ejemplos de asignación útiles. A continuación, creará su propia aplicación con mapas y los configurará mediante un asistente y desde cero.

Map Region es una función APEX nativa presentada en APEX 21.1 que proporciona la capacidad de configurar mapas interactivos que muestran datos espaciales de Oracle Spatial, GeoJSON y coordenadas. Este taller se centra en el uso de Oracle Spatial como origen de datos espaciales, para que tanto los datos espaciales raw como los resultados del análisis espacial se incorporen fácilmente.

![Aplicación de mapas de ejemplo](./images/intro-01.png "Oracle Application Express - Aplicación de Mapas de Ejemplo ")

Tiempo de taller estimado: 1 hora 15 minutos

### Acerca de Oracle Application Express (APEX) y Oracle Spatial

Oracle Application Express (APEX) y Oracle Spatial son funciones de Oracle Database, incluidos los servicios Autonomous Data Warehouse (ADW) y Autonomous Transaction Processing (ATP).

Oracle Application Express (APEX) es una plataforma de desarrollo con poco código que le permite crear aplicaciones empresariales seguras y escalables, con funciones de primera clase, que se pueden desplegar en cualquier lugar y se pueden utilizar en cualquier lugar. Más información en la [página inicial del producto Oracle APEX](https://apex.oracle.com)

Oracle Spatial es un conjunto de capacidades de gestión, análisis y procesamiento de datos geoespaciales dentro de Oracle Database. Con un tipo de datos espacial nativo y operaciones de análisis, el análisis basado en la ubicación es la corriente principal y se encuentra junto con todas las demás operaciones de base de datos. Más información en la [página inicial del producto Oracle Spatial](https://www.oracle.com/database/spatial)

### Objetivos

*   Descripción de ejemplos de región de mapa de APEX
*   Aprenderá a crear y configurar una región de asignación
*   Aprende a incorporar el análisis de ubicación con Oracle Spatial

### Requisitos

*   Se necesita Oracle APEX 21.1+. Las capturas de pantalla de este taller se realizan con APEX 21.2. Dado que generalmente recomendamos utilizar la [última versión de APEX](https://www.oracle.com/tools/downloads/apex-downloads/), se esperan pequeñas diferencias ocasionales en la interfaz de usuario.
*   Se recomienda experiencia básica con Oracle APEX, aunque no es necesaria. Si es necesario, revise el siguiente taller introductorio de LiveLabs APEX: [Creación de una aplicación basada en tablas existentes para Oracle Autonomous Cloud Service](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=628).
*   Se recomienda experiencia básica con Oracle Spatial, aunque no es necesario. Si es necesario, revise el siguiente taller introductorio LiveLabs Spatial: [Introducción a Oracle Spatial](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=736).

_Nota: Si tiene una cuenta de **Prueba gratuita**, cuando caduque la prueba gratuita, su cuenta se convertirá en una cuenta **Siempre gratis**. No podrá realizar talleres gratuitos a menos que el entorno Siempre gratis esté disponible. **[Haga clic aquí para acceder a la página Free Tier FAQ.](https://www.oracle.com/cloud/free/faq.html)**_

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Contribuyentes**: Jayson Hanes, APEX Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, marzo de 2023