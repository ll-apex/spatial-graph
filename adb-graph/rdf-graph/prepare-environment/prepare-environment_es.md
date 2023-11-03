# Preparar el Entorno

## Introducción

Oracle Autonomous Transaction Processing (ATP) es un servicio de base de datos Oracle totalmente gestionado que cuenta con funciones de "autogestión" en Oracle Cloud Infrastructure (OCI). Se recomienda crear un usuario con permisos para utilizar Graph Studio.

La siguiente guía de prácticas muestra cómo aprovisionar un ATP y crear un usuario con permisos para Graph Studio.

Tiempo estimado: 15 minutos

### Objetivos

*   Crear una Autonomous Database en Oracle Cloud.

### Requisitos

*   Explorador Web
*   Asegúrese siempre de estar en la región y el compartimento correctos

## **Tarea 1:** conexión a Oracle Cloud

1.  En el explorador, conéctese a Oracle Cloud.

## **Tarea 2:** Aprovisionamiento de ATP

Aprovisione la base de datos de Autonomous Transaction Processing (ATP) con los siguientes pasos. Como alternativa, se puede utilizar Autonomous Data Warehouse (ADW) de forma similar.

1.  Seleccione la región asignada en la parte superior derecha de la consola de OCI.
    
2.  En el menú de hamburguesa (parte superior izquierda), seleccione Oracle Database y, a continuación, Autonomous Transaction Processing.
    

![Imagen en la que se muestra en qué parte del menú seleccionar para acceder a Autonomous Transaction Processing](./images/atp.png)

3.  Haga clic en Crear Autonomous Database.

![Imagen en la que se muestra el botón para crear una base de datos autónoma](./images/create-adb.png)

4.  Seleccione el compartimento.
    
5.  Escriba un nombre único (tal vez su nombre) para su visualización y el nombre de la base de datos. El nombre mostrado se utiliza en la interfaz de usuario de la consola para identificar su base de datos.
    

![Imagen en la que se muestra la ubicación para introducir un nombre único para la base de datos](./images/unique-name.png)

6.  Asegúrese de que el tipo de carga de trabajo Procesamiento de transacciones está seleccionado.
    
7.  Introduzca una contraseña. El nombre de usuario siempre es ADMIN. (Nota: recuerde su contraseña)
    

![Imagen en la que se muestra dónde declarar la contraseña](./images/password.png)

8.  Haga clic en Create Autonomous Database en la parte inferior.
    
    La consola mostrará que ATP se está aprovisionando. Esto tardará unos 2 o 3 minutos en completarse.
    
    Puede comprobar el estado del aprovisionamiento en la solicitud de trabajo.
    

![Imagen en la que se muestra dónde comprobar el estado de la base de datos aprovisionada](./images/status.png)

Esto concluye este laboratorio. _Ahora puede continuar con la siguiente práctica de laboratorio._

## Reconocimientos

*   **Autor**: Nicholas Cusato (Hub de especialistas de Santa Mónica)
*   **Contribuyentes**: Nicholas Cusato (Santa Monica Specialist Hub)
*   **Última actualización por/fecha**: Nicholas Cusato, febrero de 2022