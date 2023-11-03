# Configuración: ejecutar pila

## Introducción

En este laboratorio, creará una pila que ejecutará un script terraform para generar una instancia de Autonomous Database, crear un usuario de Graph y cargar el juego de datos que se utilizará.

Tiempo estimado: 5 minutos.

### Objetivos

Información sobre cómo

*   Ejecute la pila para crear una instancia de Autonomous Database, un usuario de Graph y cargar un juego de datos
*   Iniciar sesión en Graph Studio

## Tarea 1: Creación de un compartimento de OCI

[](include:iam-compartment-create-body.md)

## Tarea 2: Ejecutar pila

Las siguientes instrucciones le mostrarán cómo ejecutar una pila que creará automáticamente una instancia de Autonomous Database que contenga un usuario de gráfico y el juego de datos necesario para las consultas de gráfico de propiedades.

1.  Inicie sesión en Oracle Cloud.
    
2.  Una vez conectado, utilice este [enlace](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://objectstorage.us-ashburn-1.oraclecloud.com/p/0kMdD7Vnv0J1st_2cU-S5PYNWT4SKzOOA04XbhwltUVXnOQ7vec1JJBEGk1eOxPS/n/oradbclouducm/b/moviestream_livelab/o/MovieStream_live_lab_7_AnD.zip) para crear y ejecutar la pila.
    

> Nota: el enlace se abrirá en una nueva ficha o ventana.

3.  Se le dirigirá a esta página:

![La página de creación de pila](./images/create-stack.png)

4.  Marque la casilla "He revisado y acepto las condiciones de uso de Oracle" y seleccione su **compartimento**. Deje el resto como valor por defecto. Haga clic en **Siguiente**.

![Opción para revisar y aceptar las condiciones de uso de Oracle marcada](./images/oracle-terms.png)

5.  Seleccione el **compartimento** para crear la instancia de Autonomous Database y la **región** en la que está creando la pila para crear todos los recursos. Haga clic en **Siguiente**. Después, accederá a la página Revisar, haga clic en **Crear**.

![La página de creación de pila](./images/configure-variables.png)

6.  Accederá a la página Detalles del trabajo con un estado inicial que se muestra en naranja. El icono se volverá verde una vez que el trabajo haya finalizado correctamente.
    
    ![El trabajo se ha realizado correctamente](./images/successful-job.png)
    

## Reconocimientos

*   **Autor**: Jayant Sharma, Ramu Murakami Gutiérrez, gestión de productos
*   **Contribuyentes**: Rahul Tasker, Jayant Sharma, Ramu Murakami Gutiérrez, gestión de productos
*   **Última actualización por/fecha**: Ramu Murakami Gutiérrez, mánager de productos, febrero de 2023