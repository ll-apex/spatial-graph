# Limpiar

## Introducción

En este laboratorio, anula el despliegue de la instancia de Spatial Studio creada mediante Cloud Marketplace. Depura permanentemente todos los recursos creados como parte del despliegue de Spatial Studio desde Cloud Marketplace.

Tiempo de laboratorio estimado: 5 minutos

Vea el siguiente vídeo para una breve introducción al laboratorio.

[Opción de limpieza 2: Terminar Spatial Studio y ADB](videohub:1_1jnminp7)

### Objetivos

En esta práctica de prácticas, aprenderá a:

*   Anule el despliegue de Spatial Studio y los recursos relacionados creados desde Oracle Cloud Marketplace.

### Requisitos

*   Spatial Studio desplegado desde Cloud Marketplace

## Tarea 1: Depurar recursos desplegados

Navegue a la pila utilizada para crear la instancia de Spatial Studio.

1.  Vaya a **Servicios para desarrolladores > Pilas**.
    
    ![Ir a pilas en la consola de OCI](images/teardown-01.png)
    
2.  En el menú de acción de la pila, seleccione **Ver detalles de pila**.
    
    ![Mostrar detalles de pila](images/teardown-02.png)
    
3.  Haga clic en **Destruir**. Esto depurará los recursos creados por el despliegue de Spatial Studio Marketplace.
    
    ![Destruir pila](images/teardown-03.png)
    
4.  Confirme haciendo clic nuevamente en **Destroy** (Destruir).
    
    ![Confirmar destrucción de pila](images/teardown-04.png)
    
5.  Espere aproximadamente 3-4 minutos para que el proceso se complete. Observe el estado en la sección Jobs. Cuando el estado es **Correcto**, el desempleo se completa y se depuran todos los recursos aprovisionados por el despliegue de Spatial Studio Marketplace.
    
    ![Comprobar trabajo de destrucción](images/teardown-05.png)
    

## Tarea 2: Supresión de la pila (opcional)

La pila es el juego de instrucciones para el despliegue. Captura la configuración seleccionada al ejecutar el asistente de Cloud Marketplace. Ahora que ha depurado los recursos creados al ejecutar la pila para crear la instancia de Spatial Studio, puede suprimir la pila en sí. Después de suprimir la pila, para volver a desplegar Spatial Studio, deberá empezar de nuevo con Cloud Marketplace. También puede mantener la pila y volver a ejecutarla tal cual o editarla para modificar parámetros como agregar una clave SSH para crear una instancia a largo plazo.

1.  En el menú **Más acción** de la pila, seleccione **Suprimir pila**.
    
    ![Seleccionar supresión de pila](images/teardown-06.png)
    
2.  Cuando se le solicite confirmación, haga clic en **Suprimir**.
    
    ![Confirmar supresión de pila](images/teardown-07.png)
    
3.  Todos los artefactos creados por el asistente de Cloud Marketplace, tanto los recursos como la pila, han desaparecido.
    

## Más información

*   [Página del producto Oracle Spatial](https://www.oracle.com/database/spatial)
*   [Introducción a Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)
*   [Documentación de Spatial Studio](https://docs.oracle.com/en/database/oracle/spatial-studio)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Contribuyentes**: Jesús Vizcarra
*   **Última actualización por/fecha**: David Lapp, agosto de 2023