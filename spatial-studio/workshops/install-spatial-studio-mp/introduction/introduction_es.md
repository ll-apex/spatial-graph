# Introducción

## Acerca de este taller

En este taller, aprovisionará Spatial Studio en Oracle Cloud desde OCI Cloud Marketplace y preparará un esquema en Autonomous Database para utilizarlo como repositorio de metadatos de Spatial Studio.

Tiempo de taller estimado: 60 minutos

### Acerca de Oracle Spatial Studio

Oracle Spatial Studio (Spatial Studio) es una aplicación web que proporciona acceso de autoservicio a las capacidades espaciales de Oracle Database. Si bien estas capacidades han requerido históricamente la codificación y/o el uso de herramientas de 3a parte, Spatial Studio permite a los usuarios empresariales crear y compartir análisis espaciales y mapas web interactivos utilizando GUI de autoservicio.

![Texto alternativo de imagen](./images/spatial-studio.png "Estudio espacial")

Spatial Studio funciona con datos espaciales en Oracle Database, es decir, tablas y vistas que incluyen el tipo de dato de geometría de Oracle. Estos datos son datos espaciales preexistentes o datos no espaciales que se preparan con Spatial Studio para agregar geometrías basadas en atributos.

Spatial Studio es una aplicación Java EE que se puede desplegar en Oracle Cloud desde Oracle Cloud Marketplace. Spatial Studio también se puede desplegar manualmente en Oracle WebLogic o Jetty, o como inicio rápido predesplegado independiente para realizar pruebas.

Para obtener más información, visite \[https://oracle.com/goto/spatialstudio\] (https://oracle.com/goto/spatialstudio)

### Objetivos

*   Aprender a crear y asignar un esquema de base de datos para el repositorio de metadatos de Spatial Studio
*   Descubra cómo utilizar Cloud Marketplace para instalar Spatial Studio
*   Aprender a desinstalar Spatial Studio cuando ya no sea necesario

### Requisitos

*   Este taller requiere una instancia de Oracle Autonomous Database.
*   SQL Developer Web se proporciona con Autonomous Database y también se utiliza para crear el esquema de repositorio de Spatial Studio.
*   Si ya tiene acceso a estos, puede pasar al laboratorio 3 siguiendo esta introducción.
*   De lo contrario, debe continuar con el laboratorio 1.
*   No se requiere experiencia previa con Oracle Spatial.
*   Una cuenta de Oracle Cloud: consulte la página de llegada LiveLabs de este taller para ver qué entornos están soportados

_Nota: Si tiene una cuenta de **Prueba gratuita**, cuando caduque la prueba gratuita, su cuenta se convertirá en una cuenta **Siempre gratis**. No podrá realizar talleres gratuitos a menos que el entorno Siempre gratis esté disponible. **[Haga clic aquí para acceder a la página Free Tier FAQ.](https://www.oracle.com/cloud/free/faq.html)**_

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, Database Product Management, enero de 2021