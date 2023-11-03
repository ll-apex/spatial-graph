# Introducción a los gráficos RDF

## Introducción

En este laboratorio se muestran los pasos para empezar a cargar los datos de RDF en un cubo que se enlazará a Autonomous Database. Para ello, es necesario copiar el nombre de usuario de OCI correcto del perfil. Para permitir que Graph Studio acceda a los datos de RDF en OCI Object Storage (mediante el paquete DBMS\_CLOUD), debe crear un token de acceso mediante su cuenta de OCI. Se utilizará en el laboratorio secundario.

Tiempo estimado: 5 minutos

### Objetivos

*   Carga de datos de RDF en OCI Object Storage
*   Visualización del nombre de usuario de OCI
*   Generar token de acceso

### Requisitos

En este laboratorio se asume que tiene:

*   Cuenta de Oracle Cloud
*   Descargue el archivo MOVIESTREAM (moviestream\_rdf.nt) mediante este [enlace](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)

## **Tarea 1:** cargar datos de RDF en OCI Object Storage

1.  Inicie sesión en la consola de OCI con sus credenciales de Oracle Cloud.
2.  Abra el menú de navegación y haga clic en Storage. En Object Storage y Archive Storage, haga clic en Buckets como se muestra: ![Imagen que describe dónde se ha seleccionado la carpeta de cubos en el menú](./images/buckets-folder.png)
3.  Seleccione un compartimento que se aplique a su cuenta de OCI. ![Imagen en la que se muestra dónde está el menú desplegable Compartimento en la página Cubos](./images/compartment-menu.png)
4.  Haga clic en Create Bucket. El control deslizante Create Bucket se abre como se muestra: ![Imagen que describe la página Crear cubo](./images/create-bucket.png)
5.  Introduzca el nombre del cubo, deje todo lo demás como valor por defecto y haga clic en Create. El cubo se crea y se muestra en la página Cubos como se muestra: ![Imagen en la que se muestra el resultado de la creación de un cubo](./images/bucket-result.png)
6.  Haga clic en el enlace RDF\_DATA\_BUCKET y navegue a la página Detalles de cubo.

![Imagen en la que se muestra la página Cubo después de la creación](./images/bucket-page.png) 7. Haga clic en Upload en la sección Objects. Se abre el control deslizante Cargar objetos. 8. Seleccione el [enlace](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt) del archivo RDF moviestream\_rdf.nt descargado en el sistema local y haga clic en Cargar. El archivo se carga correctamente. Haga clic en Close para volver a la página Bucket Details. El archivo cargado se muestra en Objetos como se muestra: ![Imagen en la que se muestra el objeto cargado en el cubo](./images/image-upload.png)

1.  Seleccione el menú Acciones del archivo cargado y haga clic en Ver detalles de objeto para acceder a las propiedades del archivo cargado. El control deslizante Object Details se abre como se muestra: ![Imagen en la que se muestra el menú Objeto resaltando la opción Ver detalles de objeto](./images/object-details.png)
2.  Observe la ruta de URL del objeto. Se utiliza en el asistente de importación de RDF en Graph Studio. ![Imagen en la que se muestra dónde encontrar la ruta de URL al objeto en el cubo](./images/url-path.png)

## **Tarea 2:** visualización del nombre de usuario de OCI

1.  Haz clic en el icono del avatar en la esquina superior derecha para abrir tu perfil. La primera entrada en Profile es su nombre de usuario de OCI. ![Imagen en la que se muestra cómo acceder al perfil de OCI](./images/oci-profile.png)
2.  Anote su nombre de usuario de OCI. Se utiliza en el asistente de importación de RDF en Graph Studio. ![Imagen en la que se muestra el nombre de usuario de OCI desde User Details](./images/oci-username.png)

## **Tarea 3:** generación de un token de acceso desde la consola de OCI

1.  Inicie sesión en la consola de OCI con sus credenciales de Oracle Cloud.
    
2.  Haga clic en el icono de avatar en la esquina superior derecha para abrir su perfil y haga clic en Configuración de usuario. ![Imagen en la que se muestra cómo acceder a la configuración de usuario desde el perfil](./images/user-settings.png)
    
3.  Haga clic en Tokens de autenticación en Recursos como se muestra: ![Imagen en la que se muestra cómo acceder a los tokens de autenticación desde el menú Recursos de Configuración de usuario](./images/auth-tokens.png)
    
4.  Haga clic en Generate Token. Se abre el cuadro de diálogo Generar token. ![Imagen en la que se muestra cómo generar un token de autenticación](./images/gen-tokens.png)
    
5.  Introduzca una descripción y haga clic en Generate Token. Los detalles del token generado se muestran como se muestra: ![Imagen en la que se muestra cómo copiar el token de autenticación generado](./images/token-details.png)
    
6.  Haga clic en Copy para copiar el token y guardarlo para su uso posterior.
    

Esto concluye este laboratorio. _Ahora puede continuar con la siguiente práctica de laboratorio._

## Reconocimientos

*   **Autor**: Melliyal Annamalai, mánager de productos distinguido
*   **Colaborador técnico** - Nicholas Cusato, Centro de especialistas de Santa Mónica
*   **Última actualización por/fecha**: Nicholas Cusato, Centro de especialistas de Santa Mónica, 25 de febrero de 2022