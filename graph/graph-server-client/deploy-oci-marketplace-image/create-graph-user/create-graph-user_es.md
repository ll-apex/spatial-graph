# Creación y activación de un usuario de base de datos en Database Actions

## Introducción

Este laboratorio le guiará por los pasos necesarios para empezar a utilizar Database Actions. Aprenderá a crear un usuario en Database Actions y a proporcionarle el acceso a Database Actions.

Tiempo estimado: 3 minutos

### Objetivos

*   Descubra cómo configurar los roles de base de datos necesarios en Database Actions.
*   Descubra cómo crear un usuario de base de datos en Database Actions.

### Requisitos

*   Cuenta en la nube de Oracle
*   Instancia de Autonomous Database aprovisionada

## Tarea 1: Conexión a Database Actions

Conéctese como usuario administrador en Database Actions de la instancia de ADB recién creada.

Haga clic en el **menú de navegación** en la parte superior izquierda, vaya a **Oracle Database** y seleccione **Autonomous Transaction Processing**.

![base de datos-atp](https://oracle-livelabs.github.io/common/images/console/database-atp.png)

En la página Detalles de Autonomous Database, abra el separador **Herramientas** y haga clic en **Acciones de base de datos**. Asegúrese de que su brower permita ventanas emergentes.

![consola de adb](images/adb-console.jpg)

Introduzca **ADMIN** como nombre de usuario y continúe.

![inicio de sesión-1](images/login-1.jpg)

Introduzca la contraseña (configurada en el laboratorio 2) e inicie sesión.

![inicio de sesión-2](images/login-2.jpg)

Vaya al menú **SQL** una vez que se haya conectado como usuario **ADMIN**.

![acciones de base de datos](images/database-actions.jpg)

## Taks 2: Crear roles de base de datos

Ahora cree los roles necesarios para la función de gráfico. Introduzca los siguientes comandos en la hoja de trabajo de SQL y ejecútela mientras está conectado como usuario administrador.

    <copy>
    DECLARE
      PRAGMA AUTONOMOUS_TRANSACTION;
      role_exists EXCEPTION;
      PRAGMA EXCEPTION_INIT(role_exists, -01921);
      TYPE graph_roles_table IS TABLE OF VARCHAR2(50);
      graph_roles graph_roles_table;
    BEGIN
      graph_roles := graph_roles_table(
        'GRAPH_DEVELOPER',
        'GRAPH_ADMINISTRATOR',
        'PGX_SESSION_CREATE',
        'PGX_SERVER_GET_INFO',
        'PGX_SERVER_MANAGE',
        'PGX_SESSION_READ_MODEL',
        'PGX_SESSION_MODIFY_MODEL',
        'PGX_SESSION_NEW_GRAPH',
        'PGX_SESSION_GET_PUBLISHED_GRAPH',
        'PGX_SESSION_COMPILE_ALGORITHM',
        'PGX_SESSION_ADD_PUBLISHED_GRAPH');
      FOR elem IN 1 .. graph_roles.count LOOP
      BEGIN
        dbms_output.put_line('create_graph_roles: ' || elem || ': CREATE ROLE ' || graph_roles(elem));
        EXECUTE IMMEDIATE 'CREATE ROLE ' || graph_roles(elem);
      EXCEPTION
        WHEN role_exists THEN
          dbms_output.put_line('create_graph_roles: role already exists. continue');
        WHEN OTHERS THEN
          RAISE;
        END;
      END LOOP;
    EXCEPTION
      when others then
        dbms_output.put_line('create_graph_roles: hit error ');
        raise;
    END;
    /
    </copy>
    

Asigne los permisos por defecto a los roles, **GRAPH\_ADMINISTRATOR** y **GRAPH\_DEVELOPER**, para agrupar varios permisos.

    <copy>
    GRANT PGX_SESSION_CREATE TO GRAPH_ADMINISTRATOR;
    GRANT PGX_SERVER_GET_INFO TO GRAPH_ADMINISTRATOR;
    GRANT PGX_SERVER_MANAGE TO GRAPH_ADMINISTRATOR;
    GRANT PGX_SESSION_CREATE TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_NEW_GRAPH TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_GET_PUBLISHED_GRAPH TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_MODIFY_MODEL TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_READ_MODEL TO GRAPH_DEVELOPER;
    </copy>
    

## Tarea 3: Crear un usuario de base de datos

Ahora cree el usuario **CUSTOMER\_360** y proporcione acceso a Database Actions para este usuario.

Abra el menú principal y haga clic en "Database Users".

![usuario-1](images/user-1.jpg)

Haga clic en el botón **Crear usuario**, introduzca el nombre de usuario y la contraseña. Active **Acceso web** y establezca la cuota en **UNLILMITED**.

![usuario-2](images/user-2.png)

Vaya al separador **Roles otorgados** y otorgue el rol **`GRAPH_DEVELOPER`** y el rol **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** a este usuario. (Dos roles **CONNECT** y **RESOURCE** están seleccionados por defecto. Por favor, manténgalos controlados para que también se les otorgue.)

![usuario-3](images/user-3.png)

Continúe con **Crear usuario** y abra la ventana de conexión.

![usuario-4](images/user-4.jpg)

Confirme que puede conectarse con el nuevo usuario.

![usuario-5](images/user-5.jpg)

Para obtener más información, consulte la sección ["Cómo Proporcionar Acceso a Database Actions a los Usuarios de la Base de Datos"](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/sql-developer-web.html#GUID-4B404CE3-C832-4089-B37A-ADE1036C7EEA) en la documentación.

Ahora puede pasar a la siguiente práctica de laboratorio.

## Reconocimientos

*   **Autor**: Jayant Sharma, mánager de productos, Spatial and Graph
*   **Contribuyentes** - Arabella Yao, Jenny Tsai
*   **Última actualización por/fecha**: Ryota Yamanaka, marzo de 2023