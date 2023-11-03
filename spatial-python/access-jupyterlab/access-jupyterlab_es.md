# Acceda a JupyterLab

## Introducción

Los blocs de notas son documentos interactivos para código, texto descriptivo y visualizaciones. En este taller, utilizará el código abierto JupyterLab, que proporciona un entorno de bloc de notas basado en web con muchas funciones fáciles de utilizar, como la carga de archivos.

Tiempo de laboratorio estimado: 5 minutos

### Objetivos

*   Verifique el acceso a JupyterLab
*   Exploración de la funcionalidad de Notebook
*   Seleccione la opción para realizar el resto del laboratorio práctico

## Tarea 1: Recuperar dirección IP para JupyterLab

1.  En el menú principal, vaya a Compute > Instances

![Recuperación de la dirección IP](images/compute-01.png)

2.  En la página de instrucciones del taller, haga clic en **Ver información de conexión** en la parte superior izquierda y copie el nombre del compartimento.

![Recuperación de la dirección IP](images/compartment.png)

1.  En la consola de OCI, pegue el nombre del compartimento y selecciónelo en la lista desplegable.

![Recuperación de la dirección IP](images/compute-02.png)

4.  Anote la IP pública de su instancia informática. JupyerLab se ha definido en esta instancia. Utilizará esto más adelante en esta y otras prácticas.

![Recuperación de la dirección IP](images/compute-03.png)

## Tarea 2: Verificar el acceso a JupyterLab

1.  Abra un nuevo separador del explorador e introduzca la URL **http://\[IP address\]:8001/lab**, donde \[IP address\] es la dirección recuperada en la tarea 1.
    
    ![Acceda a JupyterLab](images/access-jupyter-01.png)
    
2.  Introduzca la contraseña **livelabs** y haga clic en **Iniciar sesión**.
    

## Tarea 2: Exploración de blocs de notas de Jupyter

Jupyter Notebook es una herramienta interactiva basada en la web que permite crear y compartir documentos que contienen código activo, ecuaciones, visualizaciones y texto. Es ampliamente utilizado en la comunidad de ciencia de datos para la creación de prototipos y el análisis de datos.

En esta tarea, analizaremos los conceptos básicos del uso de Jupyter Notebook.

1.  Cree un nuevo Notebook.
    
    Cuando se cargue el entorno de Jupyter, debería ver un separador del programa de ejecución abierto.
    
    ![El separador Launcher está abierto](./images/launcher1.png)
    
    Si no ve la ventana del programa de ejecución, seleccione el archivo en la parte superior izquierda de la ventana y seleccione 'Nuevo programa de ejecución'.
    
    ![Abrir nuevo separador Iniciador](./images/launcher2.png)
    
    En la ventana del programa de ejecución, seleccione "Python 3" para crear un nuevo bloc de notas con el lenguaje de programación Python. Se creará un nuevo bloc de notas y podrá empezar a trabajar en él introduciendo código en las celdas de código o agregando texto de anotación en las celdas de anotación.
    
    ![Crear un nuevo bloc de notas de Python](./images/launcher3.png)
    
2.  Agregue texto de rebaja.
    
    Haga clic en la celda de código y utilice el menú desplegable de tipo de celda para seleccionar 'Marcado'
    
    ![Agregar celda de rebaja](./images/notebook1.png)
    
    Pegue lo siguiente en la celda y haga clic en el botón de reproducción de la barra de herramientas o pulse Shift+Enter para ejecutar la celda.
    
        	<copy>
        	# My First Notebook
        	This is my first Jupyter notebook
        	</copy>
        
    
    ![Resultado de rebaja](./images/notebook2.png)
    
3.  Escribe código Python. Pegue lo siguiente en la siguiente celda y ejecútelo. La frase "¡Hola, mundo!" debería aparecer debajo de la celda.
    
        	<copy>
        	print('Hello, World!')
        	</copy>
        
        
    
    ![hola mundo ejemplo](./images/notebook3.png)
    
4.  Para guardar un bloc de notas de Jupyter, haga clic en el icono "Guardar" de la barra de herramientas o pulse Ctrl+S (o Cmd+S en macOS). El bloc de notas se guardará con la extensión de archivo .ipynb.
    

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Contribuyentes**: Rahul Tasker, Denise Myrick, Ramu Gutiérrez
*   **Última actualización por/fecha**: David Lapp, agosto de 2023