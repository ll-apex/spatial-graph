/\* ELIMINAR ESTE ARCHIVO EN LA PRÓXIMA LIBERACIÓN - POR FAVOR USE ADB-PROVISION-CONDITIONAL.MD FILE INSTEAD Y ESPECIFICAR LA VERSIÓN QUE QUIERE EN SU MANIFEST: { "title": "Laboratorio 1: Aprovisionamiento de una instancia de ADB", "descripción": "Aprovisionamiento de una instancia de Autonomous Database", "type": "livelabs", "filename": "https://oracle-livelabs.github.io/adb/shared/adb-provision/adb-provision-conditional.md" }, \*/

# Aprovisionamiento de una instancia de Autonomous Database (ADW y ATP)

## Introducción

En este laboratorio se muestran los pasos para empezar a utilizar Oracle Autonomous Database (Autonomous Data Warehouse \[ADW\] y Autonomous Transaction Processing \[ATP\]) en Oracle Cloud. En este laboratorio, aprovisionará una nueva instancia de ADW.

> **Nota:** Si bien este ejercicio práctico utiliza ADW, los pasos son idénticos para crear una base de datos ATP.

Tiempo estimado: 5 minutos

### Objetivos

*   Descubra cómo aprovisionar una nueva instancia de Autonomous Database

## Tarea 1: Selección de ADW o ATP desde el menú Servicios

1.  Inicie sesión en Oracle Cloud.
    
2.  Una vez que haya iniciado sesión, accederá al panel de control de servicios en la nube, donde podrá ver todos los servicios disponibles. Haga clic en el menú de navegación en la parte superior izquierda para mostrar las opciones de navegación de nivel superior.
    
    > **Nota:** También puede acceder directamente al servicio Autonomous Data Warehouse o Autonomous Transaction Processing en la sección **Acciones rápidas** del panel de control.
    
    ![Página inicial de Oracle.](./images/Picture100-36.png " ")
    
3.  Los siguientes pasos se aplican de forma similar a Autonomous Data Warehouse o Autonomous Transaction Processing. En este laboratorio se muestra el aprovisionamiento de una base de datos de Autonomous Data Warehouse, por lo que haga clic en **Autonomous Data Warehouse**.
    
    ![Haga clic en Autonomous Data Warehouse.](https://oracle-livelabs.github.io/common/images/console/database-adw.png " ")
    
4.  Asegúrese de que el tipo de carga de trabajo es **Almacén de datos** o **Todo** para ver las instancias de Autonomous Data Warehouse. Utilice el menú desplegable **Ámbito de lista** para seleccionar un compartimento. Introduzca la primera parte del nombre de usuario, por ejemplo, `LL185` en el campo Search Compartments para localizar rápidamente el compartimento.
    
    ![Compruebe el tipo de carga de trabajo de la izquierda.](images/livelabs-compartment.png " ")
    
5.  Esta consola muestra que aún no existen bases de datos. Si hubiera una lista larga de bases de datos, podría filtrar la lista por el **Estado** de las bases de datos (Disponible, Parado, Terminado, etc.). También puede ordenar por **Tipo de carga de trabajo**. Aquí, se selecciona el tipo de carga de trabajo del **almacén de datos**.
    
    ![Consola de bases de datos autónomas.](./images/Compartment.png " ")
    

## Tarea 2: Creación de la instancia de ADB

1.  Haga clic en **Crear Autonomous Database** para iniciar el proceso de creación de la instancia.
    
    ![Haga clic en Crear Autonomous Database.](./images/Picture100-23.png " ")
    
2.  Aparecerá la pantalla **Create Autonomous Database**, donde especificará la configuración de la instancia.
    
    ![](./images/create-adb-screen-livelabs-default.png " ")
    
3.  Proporcione información básica para la base de datos autónoma:
    
    *   **Seleccionar un compartimento**: deje el compartimento por defecto.
    *   **Display Name**: introduzca un nombre fácil de recordar para que se muestre la base de datos. Para esta práctica de laboratorio, utilice **ADW Finance Mart**.
    *   **Nombre de base de datos**: utilice solo letras y números, empezando por una letra. La longitud máxima es de 14 caracteres. (Los caracteres de subrayado no se admiten inicialmente). Para esta práctica de laboratorio, utilice **ADWFINANCE** y **anexe su ID de usuario**. Por ejemplo, si el ID de usuario es **LL-185**, introduzca **ADWFINANCE185**
    
    ![Introduzca los detalles necesarios.](./images/Picture100-26-livelabs.png " ")
    
4.  Seleccione un tipo de carga de trabajo. Seleccione el tipo de carga de trabajo para la base de datos entre las siguientes opciones:
    
    *   **Data Warehouse**: para este laboratorio, seleccione **Data Warehouse** como tipo de carga de trabajo.
    *   **Procesamiento de transacciones**: de manera alternativa, podría haber elegido Procesamiento de transacciones como el tipo de carga de trabajo.
    
    ![Seleccionar un tipo de carga de trabajo.](./images/Picture100-26b.png " ")
    
5.  Seleccione un tipo de despliegue. Seleccione el tipo de despliegue para la base de datos de entre las opciones:
    
    *   **Shared Infrastructure**: para esta práctica de laboratorio, seleccione **Shared Infrastructure** como tipo de despliegue.
    *   **Infraestructura dedicada**: también puede haber elegido Infraestructura dedicada como tipo de despliegue.
    
    ![Seleccione un tipo de despliegue.](./images/Picture100-26_deployment_type.png " ")
    
6.  Configure la base de datos:
    
    *   **Siempre gratis**: si su cuenta en la nube es una cuenta Siempre gratis, puede seleccionar esta opción para crear una base de datos autónoma siempre gratuita. Una base de datos siempre gratis viene con 1 CPU y 20 GB de almacenamiento. Para este laboratorio, le recomendamos que deje Siempre gratis sin marcar.
    *   **Seleccionar la versión de base de datos**: seleccione una versión de base de datos de las versiones disponibles.
    *   **Recuento de OCPU**: número de CPU para el servicio. Para este laboratorio, especifique **1 CPU**. Si elige una base de datos Siempre gratis, viene con 1 CPU.
    *   **Storage (TB)** (Almacenamiento): seleccione su capacidad de almacenamiento en terabytes. Para este laboratorio, especifique **1 TB** de almacenamiento. O bien, si elige una base de datos Siempre gratis, viene con 20 GB de almacenamiento.
    *   **Escala automática**: en este laboratorio, mantenga activada la escala automática para permitir que el sistema utilice automáticamente hasta tres veces más recursos de CPU y de E/S para satisfacer la demanda de cargas de trabajo.
    *   **New Database Preview**: si aparece una casilla de control para obtener una vista previa de una nueva versión de la base de datos, NO la marque.
    
    > **Nota:** No puede ampliar ni reducir verticalmente una base de datos autónoma Siempre gratis.
    
    ![Seleccione los parámetros restantes.](./images/Picture100-26c.png " ")
    
7.  Cree las credenciales de administrador:
    
    *   **Password y Confirmar Contraseña**: especifique la contraseña para el usuario ADMIN de la instancia de servicio. La contraseña debe cumplir los siguientes requisitos:
    *   La contraseña debe tener entre 12 y 30 caracteres de longitud y debe incluir al menos una letra en mayúsculas, una letra en minúsculas y un carácter numérico.
    *   La contraseña no puede contener el nombre de usuario.
    *   La contraseña no puede contener comillas dobles (").
    *   La contraseña debe ser diferente a las 4 últimas contraseñas utilizadas.
    *   La contraseña no debe ser la misma que se haya establecido hace menos de 24 horas.
    *   Vuelva a introducir la contraseña para confirmarla. Anote esta contraseña.
    
    ![Introduzca la contraseña y confírmela.](./images/Picture100-26d.png " ")
    
8.  Seleccionar acceso de red:
    
    *   Para esta práctica de laboratorio, acepte el valor por defecto, "Secure access fromwhere".
    *   Si desea permitir el tráfico solo desde las direcciones IP y las VCN que especifique, donde el acceso a la base de datos desde todas las IP públicas o VCN está bloqueado, seleccione "Acceso seguro solo desde IP permitidas y VCN" en el área de acceso de red Choose.
    *   Si desea restringir el acceso a un punto final privado de una VCN de OCI, seleccione "Private endpoint Access only" en el área Choose Network Access.
    *   Si se selecciona la opción "Require mutual TLS (mTLS) authentication", se necesitará mTLS para autenticar las conexiones a su instancia de Autonomous Database. Las conexiones TLS permiten conectarse a su instancia de Autonomous Database sin una cartera, si utiliza un controlador JDBC Thin con JDK8 o superior. Consulte la [documentación de opciones de red](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/support-tls-mtls-authentication.html#GUID-3F3F1FA4-DD7D-4211-A1D3-A74ED35C0AF5) para conocer las opciones para permitir TLS o requerir solo autenticación TLS mutua (mTLS).
    
    ![Seleccione el acceso de red.](./images/Picture100-26e.png " ")
    
9.  Seleccione un tipo de licencia. En este laboratorio, seleccione **Traiga su propia licencia (BYOL)**. Los dos tipos de licencia son:
    
    *   **Bring su propia licencia (BYOL)**: seleccione este tipo si su organización ya dispone de licencias de base de datos.
    *   **Licencia incluida**: seleccione este tipo cuando desee suscribirse a nuevas licencias de software de base de datos y al servicio de base de datos en la nube.
    
    ![Haga clic en Crear Autonomous Database.](./images/Picture100-27-byol.png " ")
    
10.  Para esta práctica, no proporcione una dirección de correo electrónico de contacto. El campo "Contact Email" le permite mostrar contactos para que reciban avisos y anuncios operativos, así como notificaciones de mantenimiento sin planificar.
    
    ![No proporcione una dirección de correo electrónico de contacto.](images/contact-email-field.png)
    
11.  Haga clic en **Crear Autonomous Database**.
    
12.  La instancia comenzará a aprovisionarse. En unos minutos, el estado pasará de Aprovisionamiento a Disponible. En este punto, la base de datos de Autonomous Data Warehouse está lista para su uso. Consulte los detalles de la instancia aquí, incluidos el nombre, la versión de la base de datos, el recuento de OCPU y el tamaño de almacenamiento.
    

    ![Database instance homepage.](./images/Picture100-32.png " ")
    

_Continúe con el siguiente laboratorio_.

## Más información

Haga clic [aquí](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3) para obtener documentación sobre el flujo de trabajo típico para utilizar Autonomous Data Warehouse.

## Reconocimientos

*   **Autor**: Nilay Panchal, ADB Product Management
*   **Adaptado para la nube por**: Richard Green, desarrollador principal, Database User Assistance
*   **Contribuyentes**: equipo de control de calidad de Oracle LiveLabs (Jeffrey Malcolm Jr, interno | Arabella Yao, interna de mánager de productos)
*   **Última actualización por/fecha**: Richard Green, febrero de 2022