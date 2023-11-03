# Crear claves SSH en Cloud Shell

## Introducción

Para acceder a los recursos informáticos del host de Python, necesitará un par de claves SSH. Oracle Cloud Infrastructure (OCI) Cloud Shell es un terminal basado en explorador web al que se puede acceder desde la consola de Oracle Cloud que proporciona acceso a un shell de Linux. Creará su par de claves SSH en OCI Cloud Shell.

Tiempo de laboratorio estimado: xx minutos

### Objetivos

*   Cree un par de claves SSH con OCI Cloud Shell.

### Requisitos

*   Conectado a la consola de OCI.

## Tarea 1: Creación de un par de claves SSH

1.  Abrir Cloud Shell ![Abrir Cloud Shell](images/sshkeys-01.png)
    
2.  Cuando se le solicite que ejecute el tutorial, escriba N e introdúzcalo. ![Abrir Cloud Shell](images/sshkeys-02.png)
    
3.  En la línea de comandos, ejecute cada una de las siguientes acciones para crear las claves SSK.
    
        <copy>
        mkdir ~/.ssh
        </copy>
        
    
          ```
        cd ~/.ssh \`\`
    
        <copy>
        ssh-keygen -b 2048 -t rsa -f my-ssh-key
        </copy>
        
    
    Cuando se le solicite la frase de contraseña, puede hacer clic en Intro para no especificar ninguna frase de contraseña y repetir para confirmar.  
    ![Crear llaves](images/sshkeys-03.png)
    
4.  En la línea de comandos, ejecute lo siguiente para ver la clave pública. Lo utilizará en un paso posterior.
    
        <copy>
        cat ~/.ssh/my-ssh-key.pub
        </copy>
        
    
    ![Ver clave pública](images/sshkeys-04.png)
    
5.  Haga clic en el icono de reducción para minimizar Cloud Shell.
    
    ![Reducir Cloud Shell](images/sshkeys-05.png)
    
6.  Observe el botón Restore para volver a abrir Cloud Shell. Volverá a abrir Cloud Shell en un paso posterior.
    
    ![Restaurar Cloud Shell](images/sshkeys-06.png)
    

Ahora puede **proceder al siguiente laboratorio**.

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, Database Product Management, junio de 2023