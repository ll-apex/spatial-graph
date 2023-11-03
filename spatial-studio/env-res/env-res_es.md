# Acceder a Spatial Studio

## Introducción

En este laboratorio se muestra el proceso de acceso a Oracle Spatial Studio (Spatial Studio) desde una reserva LiveLabs de Oracle. Su entorno incluye Spatial Studio y Autonomous Database. En la primera conexión a Spatial Studio, proporcionará información de conexión para Autonomous Database.

Tiempo de laboratorio estimado: 10 minutos

### Objetivos

En esta práctica de prácticas, aprenderá a:

*   Descarga la cartera en la nube para tu instancia de Autonomous Database
*   Realizar 1a conexión a Spatial Studio que proporciona información de conexión de Autonomous Database

### Requisitos

*   Una reserva LiveLabs completada para "Introducción a Oracle Spatial Studio"

## Tarea 1: Descarga de Cloud Wallet para Autonomous Database

1.  En Detalles del taller, anote el nombre de usuario, la contraseña, el compartimento y la dirección IP de Spatial Studio en la nube. A continuación, inicie la consola en la nube.

![Texto alternativo de imagen](images/1-1.png "Título de la imagen")

2.  Conéctese mediante la **conexión directa de Oracle Cloud Infrastructure** con su nombre de usuario y contraseña iniciales en la nube. Se le pedirá que cambie la contraseña por defecto.

![Texto alternativo de imagen](images/1-2.png "Título de la imagen")

3.  Vaya a **Oracle Database** y, a continuación, a **Autonomous Database**.

![Texto alternativo de imagen](images/1-3.png "Título de la imagen")

4.  En el formulario Compartimento de la izquierda, empiece a escribir el nombre del compartimento anotado anteriormente. Esto filtrará dinámicamente la lista Compartimentos. Una vez que aparezca, seleccione su compartimento. A continuación, se mostrará Autonomous Database. Haga clic en el enlace a su instancia de Autonomous Database.

![Texto alternativo de imagen](images/1-4.png "Título de la imagen")

5.  Haga clic en **Conexión a base de datos** y, a continuación, en **Descargar cartera**. Promocionará una contraseña de cartera. Introduzca cualquier cadena porque no se utilizará esta contraseña. Guarde la cartera en una ubicación conveniente en su computadora portátil, ya que la utilizará en el siguiente paso.

![Texto alternativo de imagen](images/1-5.png "Título de la imagen")

## Tarea 2: Conexión por primera vez a Spatial Studio

1.  Ahora utilizará la dirección IP de Spatial Studio que anotó anteriormente. Abre una nueva pestaña en el navegador y ve a **https://\[your Spatial Studio IP address\]:4040/spatialstudio**. Por ejemplo, si la dirección IP de Spatial Studio es 123.123.12.123, debe navegar a https://123.123.12.123:4040/spatialstudio. porque la instancia de Spatial Studio no está configurada con un certificado SSL firmado, verá una advertencia de seguridad específica del explorador. Acepte la advertencia y continúe con el sitio. En un entorno de producción se configuraría un certificado y esto no ocurriría. Inicie sesión con el usuario **admin** y la contraseña **welcome1**.

![Texto alternativo de imagen](images/2-1.png "Título de la imagen")

2.  El primer inicio de sesión en Spatial Studio le solicita que introduzca la información de conexión a la base de datos para el repositorio de metadatos de Spatial Studio. Haga clic en **Autonomous Database** y, a continuación, en **Siguiente**. En el siguiente scren, arrastre y suelte el archivo de cartera que ha descargado anteriormente y haga clic en **Aceptar**.

![Texto alternativo de imagen](images/2-2.png "Título de la imagen")

3.  Ahora se le pedirá la información de conexión de la base de datos automática. Introduzca el usuario **studio\_repo**, la contraseña **Welcome1Welcome1** y seleccione el nivel de servicio medio.

![Texto alternativo de imagen](images/2-3.png "Título de la imagen")

Spatial Studio está creando ahora sus tablas de metadatos en Autonomous Database. Esto tomará aproximadamente 30 segundos.

4.  Cuando se abra Spatial Studio, se completará la primera conexión y estará listo para continuar con el taller.

![Texto alternativo de imagen](images/2-4.png "Título de la imagen")

Ahora puede [proceder al siguiente laboratorio](#next).

## Más información

*   [Página de producto de Spatial Studio](https://oracle.com/goto/spatialstudio)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management
*   **Última actualización por/fecha**: David Lapp, Database Product Management, junio de 2021