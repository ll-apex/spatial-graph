# Crear Autonomous Database

## Introducción

Oracle Autonomous Database es un servicio de base de datos autogestionado, autoprotegido y autorreparable, incluido Oracle Spatial, con ofertas para cargas de trabajo de almacenamiento de datos y procesamiento de transacciones. No es necesario configurar ni gestionar ningún hardware ni instalar ningún software. Oracle Cloud Infrastructure se encarga de crear la base de datos, así como de realizar copias de seguridad, aplicar parches, actualizar y ajustar la base de datos. Dado que este taller se centra en un caso de uso analítico, creará un almacén de datos autónomo (ADW).

Tiempo de laboratorio estimado: 5 minutos

### Objetivos

*   Creación de una instancia de Autonomous Database

### Requisitos

*   Finalización del laboratorio 1: Acceso JupyterLab

## Tarea 1: Creación de Autonomous Database

1.  En el panel de navegación principal, seleccione **Oracle Database** y, a continuación, **Autonomous Database**. ![Navegar a Oracle Database](images/adb-01.png)
    
2.  El compartimento debe estar seleccionado. Si no es así, vuelva a seleccionarlo. A continuación, haga clic en **Crear Autonomous Database**.
    

![Seleccionar compartimento](images/adb-02.png)

1.  Para el nombre mostrado, introduzca **my-adw** y para el nombre de la base de datos, introduzca **myadw**. Deje el tipo de carga de trabajo como almacén de datos.
    
    **Nota:** Debe seleccionar el tipo de carga de trabajo Almacén de datos. Si selecciona Procesamiento de transacciones, se producirá un error de cuota.
    
    ![Crear ADW](images/adb-03.png)
    
2.  Para el tipo de despliegue, deje el valor por defecto **Serverless**. Deje también los valores por defecto para la versión (19c), el recuento de ECPU (2) y el almacenamiento (1 TB). A continuación, desplácese hacia abajo. ![Crear ADW](images/adb-04.png)
    
3.  Introduzca y confirme una contraseña para el usuario ADMIN de la base de datos. A continuación, desplácese hacia abajo. ![Crear ADW](images/adb-05.png)
    
4.  En el siguiente laboratorio, creará una conexión de Python a Autonomous Database mediante un método simple que no necesita una instalación de cliente de Oracle ni una cartera en la nube. Para utilizar este método, debe preconfigurar Autonomous Database para permitir el acceso desde la instancia informática que aloja Python. Para el acceso de red, seleccione **Acceso seguro solo de IP y VCN permitidas**. En Valores, escriba la dirección IP de cálculo de la tarea 1 del laboratorio 1. ![Crear ADW](images/adb-07.png)
    
5.  En la siguiente sección, seleccione **Traiga su propia licencia (BYOL)** y **Oracle Database Enterprise Edition (EE)**. Para los contactos, introduzca su dirección de correo electrónico. A continuación, haga clic en **Crear Autonomous Database**. ![Crear ADW](images/adb-08.png)
    
6.  Se iniciará el aprovisionamiento de ADB. ![Crear ADW](images/adb-09.png)
    
7.  Cuando se complete el aprovisionamiento, la ADB estará lista. ![Crear ADW](images/adb-10.png)
    

## Tarea 2: Seleccione la opción para realizar el resto de este laboratorio práctico

El resto de este laboratorio práctico se puede realizar con una de las siguientes opciones:

**Opción 1:** siga las instrucciones para copiar, pegar o ejecutar cada paso en el bloc de notas.

1.  Vaya al **Laboratorio 3** y, a continuación, a las prácticas posteriores.

**Opción 2:** cargue un bloc de notas incorporado con todos los pasos y ejecute cada celda.

1.  Realice el **laboratorio 3 - Tarea 1**
    
2.  Realice el **Laboratorio 4 - Tarea 1**.
    
3.  Haga clic en el siguiente enlace para descargar el portátil creado previamente: \* [prebuit-notebook.ipynb](../access-jupyterlab/files/prebuilt-notebook.ipynb)
    
4.  Haga clic en el botón Upload y seleccione el bloc de notas predefinido.
    

     ![Use prebuilt notebook](./images/prebuilt-nb-01.png)
    

5.  Haga doble clic en el bloc de notas creado previamente para abrirlo y ejecutar cada celda.

     ![Use prebuilt notebook](./images/prebuilt-nb-02.png)
    

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Contribuyentes**: Rahul Tasker, Denise Myrick, Ramu Gutiérrez
*   **Última actualización por/fecha**: David Lapp, agosto de 2023