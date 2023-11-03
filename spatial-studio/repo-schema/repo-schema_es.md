# Usuario de base de datos para repositorio de Spatial Studio

## Introducción

En este ejercicio práctico se muestra la creación del esquema de base de datos que se utilizará para el repositorio de metadatos de Spatial Studio. Este es el esquema que almacenará el trabajo que realiza en Spatial Studio, como las definiciones de juegos de datos, análisis y proyectos.

El esquema de base de datos para el repositorio de Spatial Studio puede tener técnicamente cualquier nombre. Para mantener la coherencia con otros talleres de Spatial Studio, asignamos el nombre de usuario **studio\_repo**. Tenga en cuenta que este es un nombre de usuario de base de datos y es distinto de los nombres de usuario de la aplicación Spatial Studio, como el nombre de usuario de administrador de Spatial Studio por defecto (studio\_admin) creado cuando instalamos la propia aplicación Spatial Studio.

Tiempo de laboratorio estimado: 5 minutos

### Objetivos

*   Descubra cómo crear un esquema para el repositorio de metadatos de Spatial Studio
*   Descubra cómo descargar la cartera para la conexión a la base de datos

### Requisitos

*   Una cuenta en la nube de Oracle gratuita, siempre gratuita, de pago o LiveLabs
*   Acceso a la base de datos SQL Developer Web.

## Tarea 1: Crear esquema de repositorio

1.  En SQL Developer Web, conéctese a la base de datos autónoma que se utilizará para el repositorio de Spatial Studio como usuario **admin**.
    
2.  Cree el esquema para el repositorio de Spatial Studio. El esquema puede tener cualquier nombre, pero para mantener la coherencia con otras prácticas utilizamos el nombre **studio\_repo**. Los requisitos de contraseña para Oracle Autonomous Database están [aquí](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/manage-users-create.html#GUID-72DFAF2A-C4C3-4FAC-A75B-846CC6EDBA3F). Anote la contraseña que seleccione, ya que la utilizaremos en pasos posteriores.
    
        <copy>CREATE USER studio_repo
        IDENTIFIED BY <password goes here>;</copy>
        

## Tarea 2: Asignación de Cuota de Tablespace

1.  Asigne el tablespace por defecto al esquema del repositorio de Spatial Studio. Con Autonomous Database, puede utilizar **datos** de nombre de tablespace
    
        <copy>ALTER USER studio_repo
        DEFAULT TABLESPACE data;</copy>
        
2.  Asigne la cuota de tablespace al esquema del repositorio de Spatial Studio. Los metadatos de Spatial Studio ocupan una cantidad muy pequeña de almacenamiento. Por lo tanto, la cuota se adapta principalmente a los datos de negocio almacenados en el esquema de repositorio. En este laboratorio, el valor de cuota de **250M** es correcto. También puede establecer el valor en **ilimitado** si va a experimentar con otros conjuntos de datos.
    
        <copy>ALTER USER studio_repo
        QUOTA <quota value> ON data;</copy>
        

## Tarea 3: Otorgar permisos

1.  Otorgue los siguientes permisos al usuario de esquema del repositorio de Spatial Studio
    
        <copy>
        GRANT CONNECT,
              CREATE SESSION,
              CREATE TABLE,
              CREATE VIEW,
              CREATE SEQUENCE,
              CREATE PROCEDURE,
              CREATE SYNONYM,
              CREATE TYPE,
              CREATE TRIGGER
        TO  studio_repo
        </copy>
        

El esquema studio\_repo ya está listo para su uso como repositorio de Spatial Studio.

## Tarea 4: Descargar cartera

Se necesita una cartera para que Spatial Studio se conecte al esquema de repositorio de Autonomous Database que hemos creado. Utilizaremos la cartera en el próximo laboratorio.

1.  Navegue a Autonomous Database y seleccione View Details
    
    ![Texto alternativo de imagen](images/repo-schema-1.png "Título de la imagen")
    
2.  Seleccione el separador Conexión de base de datos
    
    ![Texto alternativo de imagen](images/repo-schema-2.png "Título de la imagen")
    
3.  Haga clic en Descargar cartera... ![Texto alternativo de imagen](images/repo-schema-3.png "Título de la imagen")
    
    Se le pedirá que introduzca una contraseña para el archivo de cartera. La cartera es un único archivo zip.
    
4.  Guarde el archivo de cartera en una ubicación conveniente. Necesitará este archivo en el siguiente laboratorio.
    

Ahora puede [proceder al siguiente laboratorio](#next).

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, Database Product Management, marzo de 2023