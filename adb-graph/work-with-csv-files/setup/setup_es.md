# Configuración: ejecutar pila

## Introducción

En este laboratorio, creará una pila que ejecutará un script terraform para generar una instancia de Autonomous Database, crear un usuario de gráfico y cargar el juego de datos que se utilizará.

Tiempo estimado: 5 minutos.

Vea el siguiente vídeo para una breve introducción al laboratorio. [Tutorial](videohub:1_4lr4x8eb)

### Objetivos

Información sobre cómo

*   Ejecute la pila para crear una instancia de Autonomous Database, un usuario de Graph y cargar un juego de datos
*   Iniciar sesión en Graph Studio

## Tarea 1: Creación de un compartimento de OCI

[](include:iam-compartment-create-body.md)

## Tarea 2: Ejecutar pila

Las siguientes instrucciones le mostrarán cómo ejecutar una pila que creará automáticamente una instancia de Autonomous Database que contenga un usuario de gráfico y el juego de datos necesario para las consultas de gráfico de propiedades.

1.  Inicie sesión en Oracle Cloud.
    
2.  Una vez conectado, utilice este [enlace](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oracle-quickstart/oci-arch-graph/releases/latest/download/orm-graph-stack.zip) para crear y ejecutar la pila.
    
    > Nota: el enlace se abrirá en una nueva ficha o ventana.
    
3.  Se le dirigirá a esta página:
    
    ![La página de creación de pila](./images/create-stack.png)
    
4.  Marque la casilla "He revisado y acepto las condiciones de uso de Oracle" y seleccione el compartimento. Deje el resto como valor por defecto. Haga clic en **Siguiente**.
    
    ![Opción para revisar y aceptar las condiciones de uso de Oracle marcada](./images/oracle-terms.png)
    
5.  Seleccione el **compartimento** para crear Autonomous Database y el tipo de base de datos. Haga clic en **Siguiente**. Después, accederá a la página Revisar, haga clic en **Crear**.
    
    ![Configuración de la configuración de la pila](./images/configure-variables.png)
    
6.  Accederá a la página Detalles del trabajo con un estado inicial que se muestra en naranja. El icono se volverá verde una vez que el trabajo haya finalizado correctamente.
    
    ![El trabajo se ha realizado correctamente](./images/successful-job.png)
    
    Para ver información sobre la aplicación, haga clic en **Información de la aplicación**. Guarde el nombre de usuario y la contraseña del gráfico, ya que lo utilizará para conectarse a Graph Studio.
    
    ![Cómo ver el gráfico de nombre de usuario y contraseña](./images/graph-username-password.png)
    

## Tarea 3: Iniciar sesión en Graph studio

1.  Haga clic en **Open Graph Studio** en Application Information. Esto abrirá una nueva página. Introduzca el nombre de usuario y la contraseña del gráfico proporcionados en Información de la aplicación en la pantalla de conexión.
    
    ![Abrir estudio de gráficos en Información de aplicación](./images/login-page.png " ")
    
2.  A continuación, haga clic en el botón **Sign In** (Iniciar sesión). Debería ver la página de inicio del estudio.
    
    ![El texto alternativo no está disponible para esta imagen](./images/gs-graphuser-home-page.png " ")
    
    Graph Studio consta de un conjunto de páginas a las que se accede desde el menú de la izquierda.
    
    El icono **Inicio** le lleva a la página de inicio.  
    La página **Gráfico** muestra los gráficos existentes para su uso en blocs de notas.  
    La página **Notebook** muestra los blocs de notas existentes y le permite crear uno nuevo.  
    La página **Plantillas** permite crear plantillas para las visualizaciones de gráficos.  
    La página **Trabajos** muestra el estado de los trabajos en segundo plano y permite ver el log asociado, si lo hay.  
    

Esto concluye este laboratorio. **Ahora puede continuar con la siguiente práctica de laboratorio.**

## Reconocimientos

*   **Autor**: Jayant Sharma, Ramu Murakami Gutiérrez, gestión de productos
*   **Contribuyentes**: Rahul Tasker, Jayant Sharma, Ramu Murakami Gutiérrez, gestión de productos
*   **Última actualización por/fecha**: Ramu Murakami Gutiérrez, mánager de productos, junio de 2023