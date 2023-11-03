# Despliegue de Spatial Studio en Oracle Cloud

## Introducción

En este laboratorio, desplegará Spatial Studio desde Cloud Marketplace mediante recursos Siempre gratis. Cloud Marketplace se encarga de instalar y configurar Spatial Studio y una instancia de Autonomous Database. La instancia de Spatial Studio creada debe ser temporal para su uso durante este taller.

Tiempo de laboratorio estimado: 15 minutos

Vea el siguiente vídeo para una breve introducción al laboratorio.

[Despliegue de Spatial Studio en Oracle Cloud](videohub:1_63orvw8q)

### Objetivos

En esta práctica de prácticas, aprenderá a:

*   Despliegue Spatial Studio desde Oracle Cloud Marketplace con recursos Siempre gratis.

### Requisitos

*   Una cuenta de Oracle Cloud
*   Es administrador de la cuenta en la nube.

## Tarea 1: Verificación de la disponibilidad del recurso informático

Antes de iniciar el despliegue de Spatial Studio, es necesario verificar el dominio de disponibilidad que tiene cuota para la unidad de computación Siempre gratis.

1.  Vaya a **Gobernanza y administración > Límites, cuota y uso**.
    
    ![Comprobar límites y cuotas](images/quota-01.png)
    
2.  El menú Ámbito muestra los dominios de disponibilidad. Seleccione el primer dominio de disponibilidad, escriba **micro** en el menú Recurso y seleccione **Núcleos para Standard.E2.1. Instancias de micro VM**.
    
    ![Seleccionar unidad de computación](images/quota-02.png)
    
3.  El listado de resultados muestra el límite de servicio (cuota), el uso y la disponibilidad de la unidad seleccionada en el dominio de disponibilidad seleccionado. En el siguiente ejemplo, no hay disponibilidad para el dominio de disponibilidad seleccionado.
    
    ![Compruebe la disponibilidad de la unidad de computación seleccionada](images/quota-03.png)
    
4.  Si el dominio de disponibilidad seleccionado no tiene cuota, cambie al siguiente dominio de disponibilidad y vuelva a introducir **micro** en el menú Recurso y seleccione **Núcleos para Standard.E2.1. Instancias de micro VM**. En este caso, el segundo dominio de disponibilidad tiene cuota.
    
    ![Compruebe la disponibilidad para una unidad de computación alternativa](images/quota-04.png)
    

Tenga en cuenta que el dominio de disponibilidad tiene cuota para la unidad de computación de destino, ya que deberá seleccionarla al instalar Spatial Studio desde Cloud Marketplace.

## Tarea 2: Instalación de Spatial Studio desde Cloud Marketplace

1.  Haga clic en el icono de hamburguesa situado en la parte superior izquierda para abrir el menú de navegación principal. Seleccione **Marketplace** y, a continuación, haga clic en **Todas las aplicaciones**.
    
    ![Vaya a Oracle MarketPlace](images/mp-01.png)
    
2.  Busque **spatial** y, a continuación, haga clic en la aplicación **Oracle Spatial Studio**.
    
    **Nota:** Asegúrese de seleccionar "Oracle Spatial Studio" y no "Oracle Spatial Studio for Roving Edge Infrastructure".
    
    ![Buscar aplicación Oracle Spatial Studio](images/mp-02.png)
    
3.  Si tiene un compartimento preferido existente, selecciónelo; de lo contrario, deje el compartimento preferido por defecto (raíz). Acepte las condiciones y haga clic en **Iniciar pila**.
    
    ![Pila de inicio para Oracle Spatial Studio](images/mp-04.png)
    
4.  Acepte los valores predeterminados y haga clic en **Siguiente**.
    
    ![Definir parámetros para el despliegue de Oracle Spatial Studio](images/mp-05.png)
    
5.  Seleccione el dominio de disponibilidad con cuota, como identificó en la tarea 1. Seleccione la unidad Siempre gratis **VM.Standard.E2.1. Micro**. Si tiene créditos en la nube disponibles o una cuenta de pago, puede seleccionar una unidad de pago en su lugar.
    
    ![Más parámetros para el despliegue](images/mp-06.png)
    
    A continuación, desplácese hacia abajo.
    
6.  Por defecto, Spatial Studio solo permite el acceso HTTPS, que requiere una configuración adicional para el acceso seguro. Para este taller, desplegará una instancia temporal que no incluirá ninguna información confidencial. Por lo tanto, desmarque **Sólo HTTPS** y lea el texto de ayuda para asegurarse de que comprende el uso previsto. En Spatial Studio Admin User Name (Nombre de usuario administrador de Spatial Studio), introduzca **admin** (minúscula). Este nombre de usuario será sensible a mayúsculas/minúsculas.
    
    ![Configuración avanzada de Spatial Studio](images/mp-07.png)
    
    A continuación, desplácese hacia abajo.
    
7.  Introduzca una contraseña para el usuario administrador de Spatial Studio. Esta es la contraseña que utilizará al conectarse a Spatial Studio.
    
    ![Contraseña para el usuario administrador de Spatial Studio](images/mp-07a.png)
    
    A continuación, desplácese hacia abajo.
    
8.  En Configure Networking, deje los valores predeterminados para que se cree una red. A continuación, desplácese hacia abajo.
    
9.  Las claves SSH permiten acceder al servidor de Spatial Studio para la administración, como reiniciar la instancia y comprobar los archivos log. En este caso, la instancia de Spatial Studio es temporal y está pensada para la duración de este taller. Por lo tanto, la administración no es necesaria. Por lo tanto, **desactive** la opción **Agregar clave SSH**.
    

![Agregar clave SSH para la instancia informática utilizada por Oracle Spatial Studio](images/mp-09.png)

A continuación, desplácese hacia abajo.

10.  Spatial Studio necesita acceso a una instancia de Oracle Database. Marque la casilla Siempre gratis y acepte los demás valores por defecto para que se cree y configure una instancia de Autonomous Database. Si tiene créditos en la nube disponibles o una cuenta de pago, puede desmarcar esta casilla y seleccionar una configuración de pago en su lugar.

![Configurar la base de datos que Oracle Spatial Studio utilizará como repositorio](images/mp-11.png)

A continuación, desplácese hacia abajo.

11.  Para el nivel de servicio de base de datos autónoma, seleccione **medio**. A continuación, introduzca una contraseña para el usuario de base de datos que almacena los metadatos de Spatial Studio. Esto se utilizará en la configuración automática de metadatos para la instancia de Spatial Studio. No tendrá que volver a utilizar esta contraseña en este taller. A continuación, haga clic en **Siguiente**.

![Desplegar Spatial Studio](images/mp-12.png)

12.  Ahora está en el paso Review del asistente. Desplácese hasta la parte inferior y asegúrese de que la opción **Run apply** está marcada. A continuación, haga clic en **Crear**.

![Desplegar Spatial Studio](images/mp-13.png)

13.  Espere aproximadamente 5 minutos para que el estado cambie de IN PROCESS a SUCCEEDED.

![Desplegar Spatial Studio](images/mp-14.png)

Después de que el estado sea SUCCEEDED, **espere 5 minutos adicionales** para que los pasos posteriores a la instalación automatizados se completen antes de continuar.

## Tarea 3: Conexión a Spatial Studio

1.  Haga clic en el separador **Información de aplicación** y, a continuación, haga clic en el enlace de **URL HTTP de Spatial Studio**.
    
    ![Recuperar URL para iniciar Spatial Studio](images/mp-15.png)
    
2.  Inicie sesión con el nombre de usuario **admin** y la contraseña que introdujo en el paso 7 anterior.
    
    ![Cuadro de diálogo de conexión para Spatial Studio](images/mp-17.png)
    
3.  Una vez que haya iniciado sesión, pase el cursor sobre los iconos del panel de navegación principal de la izquierda para ver las pistas con los nombres de página.
    
    ![Página Introducción a Spatial Studio](images/mp-19.png)
    
4.  En cualquier momento también puede hacer clic en el icono "hamburguesa" en la parte superior izquierda para expandir y contraer el panel de navegación principal.
    
    ![Panel de navegación de Spatial Studio](images/mp-20.png)
    

Ya está conectado y listo para empezar a utilizar Spatial Studio.

Ahora puede **proceder al siguiente laboratorio**.

## Más información

*   [Página del producto Oracle Spatial](https://www.oracle.com/database/spatial)
*   [Introducción a Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)
*   [Documentación de Spatial Studio](https://docs.oracle.com/en/database/oracle/spatial-studio)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Contribuyentes**: Jesús Vizcarra
*   **Última actualización por/fecha**: David Lapp, agosto de 2023