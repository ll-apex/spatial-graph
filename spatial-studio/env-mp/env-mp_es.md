# Instalar Spatial Studio

## Introducción

En este laboratorio se analiza el proceso de aprovisionamiento de Oracle Spatial Studio (Spatial Studio) mediante Oracle Cloud Marketplace. Oracle Cloud Marketplace proporciona aplicaciones y servicios proporcionados por Oracle y 3eras partes. Puede encontrar más información [aquí](https://docs.oracle.com/en/cloud/marketplace/marketplace-cloud/index.html).

Tiempo de laboratorio estimado: 30 minutos

### Objetivos

En esta práctica de prácticas, aprenderá a:

*   Descubra cómo instalar Spatial Studio desde Oracle Cloud Marketplace.
*   Aprender a definir el esquema del repositorio de Spatial Studio en el inicio inicial

### Requisitos

*   Una cuenta en la nube de Oracle gratuita, siempre gratuita, de pago o LiveLabs
*   Esquema de repositorio creado (Laboratorio 3).

## Tarea 1: Seleccionar Spatial Studio de Marketplace

1.  Haga clic en el **menú de navegación** en la parte superior izquierda y seleccione **Marketplace**.

![Oracle Cloud Marketplace](https://oracle-livelabs.github.io/common/images/console/marketplace.png "Marketplace")

2.  Busque Spatial Studio y, a continuación, haga clic en la aplicación Oracle Spatial Studio.

![Oracle Spatial Studio en Oracle Cloud Marketplace.](images/env-marketplace-2.png "Imágenes de Oracle Spatial Studio Marketplace")

3.  Revise las instrucciones de uso, acepte las condiciones y haga clic en Launch Stack.

![Iniciar pila para desplegar Oracle Spatial Studio](images/env-marketplace-3.png "Iniciar pila")

## Tarea 2: Asistente de Creación de Pila

1.  También puede introducir un nombre y una descripción personalizados para la pila de despliegue. A continuación, seleccione el compartimento que desea utilizar para el despliegue y haga clic en Next

![Asistente de creación de pila](images/env-marketplace-4.png "Cree la pila utilizando el asistente.")

2.  Seleccione el dominio de disponibilidad y la unidad para la instancia informática.

Puede obtener más información sobre las unidades de computación [aquí](https://docs.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm). Compruebe la disponibilidad de cuota de la unidad que desee en los dominios de disponibilidad. Esto es especialmente importante cuando se utiliza una unidad Siempre gratis: \*En la consola de OCI, vaya a Gobernanza > Límites, cuotas y uso \* Para el servicio, seleccione Recursos informáticos y, para el ámbito, seleccione un dominio de disponibilidad \* Confirme la disponibilidad de la unidad deseada \* Cambie la selección de dominio de disponibilidad si es necesario para identificar la cuota disponible

![Límites, cuotas y uso de los recursos de Oracle Cloud](images/env-marketplace-4-1.png "Límite para recursos informáticos")

Una vez confirmada la cuota, realice las selecciones en el asistente Crear pila.

![Definir parámetros de pila](images/env-marketplace-5.png "Seleccionar instancia informática")

A continuación, desplácese hacia abajo.

3.  Opcionalmente, cambie el puerto HTTPS y el nombre de usuario administrador de Spatial Studio de los valores por defecto. Para la autenticación del usuario administrador de Spatial Studio, tiene la opción de utilizar secretos de OCI Vault o una contraseña. En la imagen siguiente se muestra un ejemplo con una contraseña. Para los despliegues de producción, se recomienda utilizar secretos de OCI Vault. Desplácese hacia abajo hasta la sección sobre la configuración de red.

Nota: Por defecto, el nombre de usuario administrador de Spatial Studio es **admin**. Se trata de un usuario de la aplicación Spatial Studio distinto del nombre de usuario de la base de datos (studio\_repo) creado en el laboratorio 3 para el esquema de repositorio almacenado en la base de datos.

![Definir más parámetros, como puerto y contraseña](images/env-marketplace-6.png "Configuración avanzada de Spatial Studio - Contraseña de usuario administrador de Spatial Studio")

4.  Para las redes, tiene la opción de crear automáticamente una nueva VCN o una existente. Seleccione el compartimento para crear una nueva VCN o buscar VCN existentes.

En la siguiente imagen se muestra un ejemplo del uso de Crear nueva VCN. Para utilizar una VCN existente, debe estar en el mismo dominio de disponibilidad que el seleccionado anteriormente en el paso 2. Si no tiene otras VCN existentes, los valores por defecto restantes se pueden dejar tal cual. Si tiene otras VCN existentes, actualice los valores de CIDR para evitar conflictos.

![Configurar la red](images/env-marketplace-7.png "Configuración avanzada de Spatial Studio - Configuración de red")

Vaya a la sección SSH Keys (Claves SSH).

5.  La carga de una clave pública SSH permite acceder al sistema de archivos de Spatial Studio con fines administrativos. El cuadro de diálogo tiene enlaces a la documentación general de conexión SSH. Envíe la clave pública SSH navegando hasta el archivo de claves o copie la cadena de claves. Si carga la clave pública SSH desde un archivo, el nombre del archivo de clave se mostrará como se muestra en la siguiente imagen. Haga clic en Next.

![Agregue la clave SSH.](images/env-marketplace-8.png "Configuración avanzada de Spatial Studio: clave SSH pública")

6.  Revise el resumen de las entradas. Si se necesitan correcciones, haga clic en Atrás. De lo contrario, haga clic en Create para iniciar el proceso de despliegue. Se le redirigirá a una página Detalles del trabajo para el despliegue.

![Crear pila](images/env-marketplace-9.png "Revisar definición de pila y crear pila")

## Tarea 3: Supervisión del progreso del despliegue

1.  La sección Logs en la parte inferior de la página Detalles del trabajo mostrará el progreso. Inicialmente se mostrará un spinner mientras se configura para el despliegue.

![Trabajo de supervisión de despliegue de pila - Aplicación de Terraform](images/env-marketplace-10.png "Supervisar progreso de despliegue de pila")

Después de unos minutos, verá la información del log.

![Registrar información sobre el trabajo de despliegue](images/env-marketplace-11.png "Log de despliegue de pila")

2.  Desplácese hasta la parte inferior de la sección de logs. Cuando haya terminado, verá Apply Complete! seguido de los detalles de la instancia. El último elemento mostrado es la URL pública de Spatial Studio. Copie esta URL y péguela en un explorador.

![El trabajo de despliegue ha finalizado correctamente](images/env-marketplace-12.png "Variables de salida para pila desplegada")

## Tarea 4: Conexión por primera vez

1.  Al abrir la URL pública de Spatial Studio por primera vez, se mostrará una advertencia del explorador relacionada con la privacidad y la seguridad. La advertencia específica depende de su plataforma y navegador.

![Advertencia al abrir la URL de Spatial Studio](images/env-marketplace-13.png "Advertencia de conexión de explorador")

Este no es un problema de Spatial Studio; es genérico para el acceso a sitios web que no tienen un certificado HTTPS firmado. La carga y configuración de un certificado firmado elimina esta advertencia. Sin embargo, el proceso de carga de certificados en Jetty está fuera del alcance de este taller.

Haga clic en el enlace para acceder al sitio web.

2.  Introduzca el nombre de usuario administrador de Spatial Studio (el valor por defecto es admin) y la contraseña introducida en el paso 2 (Asistente de creación de pila, elemento 3). A continuación, haga clic en Sign In.

![Proporcione el nombre de usuario y la contraseña para conectarse a Spatial Studio](images/env-marketplace-14.png "Cuadro de diálogo de inicio de sesión de Spatial Studio")

3.  En la primera conexión a una instancia de Spatial Studio, se le solicitará información de conexión para el esquema de base de datos que se utilizará como repositorio de metadatos de Spatial Studio. Es el esquema de base de datos utilizado para todos los metadatos de Spatial Studio y también lo pueden utilizar los usuarios administradores de Spatial Studio para almacenar otros datos. Utilizará el esquema creado en el laboratorio 3, así que seleccione Oracle Autonomous Database y haga clic en Next.

![Seleccionar tipo de conexión de metadatos](images/env-marketplace-15.png "Seleccionar tipo de repositorio de metadatos de Spatial Studio")

4.  Busque (o arrastre y suelte) el archivo Wallet guardado en el laboratorio 3. Después de la carga, el nombre del archivo de cartera se mostrará como cartera seleccionada. Haga clic en OK.

![Cargar cartera](images/env-marketplace-16.png "Cargar la cartera de conexión")

5.  Escriba el nombre de usuario y la contraseña definidos en el laboratorio 2 y el servicio. El nivel de servicio medio es adecuado para este taller. Haga clic en OK.

![Introduzca los detalles de conexión para el repositorio de metadatos](images/env-marketplace-17.png "Introducir detalles de conexión")

6.  Espere unos instantes mientras Spatial Studio realiza su conexión inicial al esquema y crea varias tablas de metadatos. Cuando termine, Spatial Studio se abrirá con la información de introducción.

![Página principal de Spatial Studio - Introducción](images/env-marketplace-18.png "Página de llegada de Spatial Studio")

## Tarea 5: Carga de datos y creación de un mapa

Para verificar que Spatial Studio funciona correctamente, cargará, preparará y visualizará una muestra de datos pequeña. Los datos contienen una lista de museos incluyendo nombre y dirección. Geocodificará los datos y los visualizará en un mapa interactivo.

1.  No creará una conexión aquí, ya que puede utilizar la conexión al repositorio de Spatial Studio para esta verificación. Haga clic en el mosaico para **Crear juego de datos**.

![Iniciar asistente para cargar datos](images/verify-1.png "Creación de un juego de datos")

2.  Descargue el archivo de ejemplo de datos [aquí](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/sf_area_museums.xlsx) y guárdelo en una ubicación conveniente. A continuación, arrastre y suelte el archivo en el mosaico de carga de archivos. También puede hacer clic en el mosaico de carga de archivos y navegar hasta el archivo.

![Crear un juego de datos mediante la carga de datos](images/verify-2.png "Cargar datos de hoja de cálculo existentes")

3.  En la vista previa de datos, defina la conexión de carga en SPATIAL\_STUDIO y defina el tipo de dato para POSTAL\_CODE en STRING. A continuación, haga clic en **Enviar**.

![Especificar detalles de carga](images/verify-3.png "Especifique los detalles de carga y compruebe la configuración de columna")

4.  Cuando se complete la carga, el juego de datos se mostrará con un ícono de advertencia que indica que se deben realizar acciones. Haga clic en el icono de advertencia y, a continuación, en el enlace **Ir a Columnas de Juego de Datos** para asignar una columna de clave.

![Definir la columna de clave para el juego de datos](images/verify-4.png "Resolver problemas de juego de datos: seleccionar o agregar columna de clave")

5.  Seleccione NAME como clave y, a continuación, haga clic en **Validate key**.

![validar clave](images/verify-5.png "Validar la clave seleccionada")

Después de validar la clave, haga clic en **Aplicar**.

6.  Vuelva a hacer clic en el icono de advertencia y, a continuación, haga clic en el botón **Direcciones Geocodificadas** para convertir direcciones para coordinar ubicaciones para la visualización de mapas.

![Geocodificar direcciones](images/verify-7.png "Resolver problemas de conjuntos de datos: direcciones de geocodificación")

7.  Observe que las columnas ADDRESS y POSTAL\_CODE se han detectado automáticamente para su uso en la geocodificación. Acepte los valores por defecto y haga clic en **Aplicar**.

![Asignación de direcciones geográficas](images/verify-8.png "Asignar juego de datos con datos de referencia de geocodificación")

Cuando se completa la geocodificación, vuelve a la página Datasets.

8.  Haga clic en el menú de acción del juego de datos SF\_AREA\_MUSEUMS y seleccione **Crear proyecto**.

![Comenzar a crear el proyecto](images/verify-9.png "Crear un proyecto nuevo para el juego de datos")

9.  Haga clic y arrastre el juego de datos SF\_AREA\_MUSEUMS y suéltelo en cualquier lugar del mapa.

![Agregar juegos de datos y arrastrarlos al lienzo de mapa](images/verify-10.png "Agregar juegos de datos como capas al proyecto")

El juego de datos SF\_AREA\_MUSEUMS se agregará como capa de mapa, y el mapa se desplazará y ampliará al área de los datos.

10.  Haga clic en el menú de acción de la capa SF\_AREA\_MUSEUMS y seleccione **Configuración**

![Configuración de la capa de datos](images/verify-11.png "Definir estilos y mucho más para la capa de datos")

11.  Dar estilo a la capa del mapa seleccionando un color y opacidad de su elección.

![Valor de estilo](images/verify-12.png "Seleccionar color y opacidad para la capa de datos")

12.  Haga clic en el separador **Interacción**, active la **ventana Mostrar información** y seleccione todas las columnas. A continuación, haga clic en un elemento del mapa para ver una ventana de información con los valores de datos del elemento seleccionado.

![Configuración para interacciones de mapa](images/verify-13.png "Definir detalles para interactuar con el mapa")

Esto verifica que la preparación y visualización de datos básica funcione correctamente.

13\. Haga clic en el botón del panel de navegación izquierdo para volver a la página Juegos de datos. Seleccione la opción **Desechar Cambios**, ya que no es necesario conservar esta prueba.

![Desechar cambios](images/verify-14.png "Desechar los cambios realizados para el proyecto actual")

14.  Una vez completada la verificación, puede suprimir la tabla de base de datos y el juego de datos de prueba. Haga clic en el menú de acción de SF\_AREA\_MUSEUMS y seleccione **Suprimir**.

![Suprimir juego de datos](images/verify-15.png "Suprimir el juego de datos")

15.  Seleccione la opción para suprimir la tabla de base de datos y haga clic en **Aceptar**.

![Seleccione esta opción para suprimir permanentemente la tabla de base de datos](images/verify-16.png "Suprimir la tabla de base de datos relacionada con el juego de datos")

Oracle Spatial Studio ahora está aprovisionado y probado. El siguiente laboratorio proporciona pasos para eliminar Spatial Studio cuando ya no sea necesario.

## Tarea 6: Desinstalación de Spatial Studio (cuando ya no sea necesario)

**Si desea eliminar completamente su despliegue de Marketplace, continúe con lo siguiente.**

1.  Haga clic en el **menú de navegación** en la parte superior izquierda, vaya a **Servicios para desarrolladores** y seleccione **Pilas**.

![Limpiar todos los recursos desplegados](https://oracle-livelabs.github.io/common/images/console/developer-resmgr-stacks.png "Eliminar despliegue de Marketplace")

2.  Seleccione el compartimento y el nombre utilizados en el PASO 2. En el ejemplo que se muestra a continuación, se ha utilizado un compartimento denominado sandbox y Stack denominado Oracle Spatial Studio.

![Seleccione el compartimento adecuado y la pila que se va a suprimir](images/env-marketplace-20.png "Seleccionar pila")

3.  Seleccione Terraform Actions > Destroy

![Destruir todos los recursos desplegados a través de la pila de Oracle Spatial Studio](images/env-marketplace-21.png "Destruir los recursos desplegados")

Se le pedirá que confirme. Esto eliminará los artefactos de Compute y Network creados por el despliegue de Marketplace.

4.  Después de eliminar la aplicación Spatial Studio, el esquema del repositorio permanece en su lugar. Para eliminar el esquema del repositorio, conéctese a la base de datos como **admin**, como se hizo en el laboratorio 3, y ejecute lo siguiente.

    <copy>DROP USER studio_repo CASCADE;</copy>
    

## Más información

*   [Página de producto de Spatial Studio](https://www.oracle.com/database/spatial/#rc30p2)
*   [Introducción a Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, Database Product Management, marzo de 2023