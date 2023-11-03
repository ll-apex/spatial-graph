# Incorporar el análisis espacial

## Introducción

En este laboratorio, mejorará el mapa del laboratorio anterior incorporando un análisis espacial. Configurará una búsqueda de aeropuertos situados a una distancia definida por el usuario de un estado seleccionado.

Tiempo de laboratorio estimado: 30 minutos

### Objetivos

*   Comprender una operación básica de análisis espacial
*   Comprender la integración del análisis espacial en la región de mapa de APEX

### Requisitos

*   Laboratorio 3: Crear un mapa desde cero

## Tarea 1: Agregar una región para filtros

1.  Haga clic en la **Página 3: Mapa de aeropuertos y estados** en la parte superior del árbol de la izquierda. A continuación, en el panel Propiedades de página de la derecha, en Apariencia, cambie la plantilla de página a **Columna izquierda**.
    
    ![Actualizar Plantilla de Página](images/add-spatial-analysis-01a.png)
    
    A continuación, debe ver **LEFT COLUMN** en el diseño.
    
    ![Actualizar Plantilla de Página](images/add-spatial-analysis-01b.png)
    
2.  Arrastre una región Static Content a la columna izquierda.
    
    ![Agregar región de contenido estático](images/add-spatial-analysis-01c.png)
    
3.  Cambie el nombre a **Región Mis filtros** o a un nombre de su elección.
    
    ![Cambiar nombre de región](images/add-spatial-analysis-02.png)
    

## Tarea 2: Agregar un elemento para la selección de estado

1.  Arrastre un elemento Select List a la región de filtros y actualice el nombre a **P3\_STATE**.
    
    ![Agregar Seleccionar Elemento de Lista](images/add-spatial-analysis-03.png)
    
2.  En las propiedades Page Item de la derecha, desplácese a la sección List of Values. Active **Valor necesario** con el conmutador, defina el tipo como **Consulta SQL** e introduzca la siguiente consulta:
    
        <copy>
          select name, state_code
            from EBA_SAMPLE_MAP_SIMPLE_STATES
        order by name
        </copy>
        
    
    ![Consulta SELECT](images/add-spatial-analysis-04.png)
    
3.  En las propiedades Page Item de la derecha, desplácese a la sección Default. Defina el tipo en **Estático** y el valor en **'Texas'** u otro estado que elija (entre comillas simples).
    
    ![Configurar lista de selección](images/add-spatial-analysis-05.png)
    

## Tarea 3: Adición de un elemento para la entrada de distancia

1.  Arrastre Number Field a la región de filtros. Actualice el nombre a **P3\_DISTANCE** y la etiqueta a **Proximity (km)**.
    
    ![Agregar elemento de campo de número](images/add-spatial-analysis-06.png)
    
2.  En las propiedades del elemento de página de la derecha, desplácese a la sección Validación y active **Valor necesario**.
    
    ![Establecer validación en valor necesario](images/add-spatial-analysis-07.png)
    
3.  Desplácese a la sección Default. Establezca el tipo en **Static** (Estática) y el valor en **100**.
    
    ![Configurar valor por defecto](images/add-spatial-analysis-08.png)
    
    Ahora tiene entradas para filtrar aeropuertos por proximidad a un estado. A continuación, aplicará los filtros mediante acciones dinámicas.
    

## Tarea 4: Aplicación de filtros mediante acciones dinámicas

A continuación, creará las acciones que se llaman cuando el usuario cambie los valores de estado y/o distancia.

1.  Haga clic con el botón derecho en el elemento P3\_STATE o P3\_DISTANCE y seleccione **Crear acción dinámica** (la acción que creamos se aplicará a ambos elementos).
    
    ![Crear acción dinámica](images/add-spatial-analysis-09.png)
    
2.  En las propiedades de acción dinámica de la derecha, defina el nombre en **Validar y refrescar**. En la sección When, establezca Event en **Change** (Cambiar), Selection Type (Tipo de selección) en **Items** (Elementos) y items en la lista separada por comas **P3\_DISTANCE,P3\_STATE** (Elementos). Tenga en cuenta que el botón situado a la derecha del cuadro de texto Elementos permite seleccionar elementos de una lista. Para evitar el envío de valores negativos para la distancia, en la sección Condición del cliente, defina Tipo en **Elemento >= Valor**, Elemento en **P3\_DISTANCE** y Valor en **0**.
    
    ![Configuración de la acción dinámica](images/add-spatial-analysis-10.png)
    
3.  Las acciones dinámicas se configuran con acciones TRUE y FALSE que se llaman en función de las condiciones que se han configurado. En este caso, la condición del cliente (P3\_DISTANCE >= 0) determina si se debe llamar a la acción TRUE (se cumple la condición) o a la acción FALSE (no se cumple la condición). Esto nos permitirá atrapar la entrada de distancia negativa.
    
    Cuando la condición del cliente es TRUE, la acción debe enviar los valores de entrada y refrescar la página. Haga clic en la acción en True. En las propiedades de acción de la derecha, en Identification set Action (Identificación), seleccione **Refresh** (Refrescar). En Elementos afectados, defina Tipo de selección en **Región** y Región en **Mi región de mapa** (o el nombre que ha utilizado si es diferente). Observe en el árbol de páginas de la izquierda que la acción Verdadero cambia a Refrescar.
    
    ![Configuración de la acción dinámica](images/add-spatial-analysis-11.png)
    
4.  A continuación, configurará la acción para llamar cuando no se cumpla la condición del cliente, lo que significa que se ha introducido un valor de distancia negativo. En Acciones dinámicas para cualquiera de los elementos, haga clic con el botón derecho en False y seleccione **Crear acción FALSE**.
    
    ![Configuración de la acción dinámica](images/add-spatial-analysis-12.png)
    
5.  La acción FALSE invocada cuando la distancia es negativa será un mensaje emergente para el usuario. Haga clic en la acción False. En las propiedades Action de la derecha, en Identification (Identificación), establezca Action (Acción) en **Alert** (Alerta). En Configuración, defina el título en **Distancia no válida** (este será el banner de alerta) y el mensaje en **Distancia debe ser >= 0** (este será el cuerpo de la alerta). Observe en el árbol de página de la izquierda que la acción False cambia a Alert.
    
    ![Configuración de la acción dinámica](images/add-spatial-analysis-13.png)
    
6.  La región de mapa incluye actualmente una capa de estados que muestra todos los estados. Ahora ajusta esta capa para mostrar solo el estado seleccionado en el menú P3\_STATE. En el árbol de páginas de la izquierda, en Layers, haga clic en States. En las propiedades de capa de la derecha, en Identification, cambie Name a **Selected State** (Estado seleccionado). En Origen, defina la cláusula Where en **state\_code = :P3\_STATE**. Observe en el árbol de páginas de la izquierda que el nombre de la capa cambia a Selected State.
    
        <copy>
        state_code = :P3_STATE
        </copy>
        
    
    ![Configurar la cláusula WHERE](images/add-spatial-analysis-14.png)
    
7.  Por último, actualice la capa Aeropuertos para devolver los artículos filtrados por el estado y la proximidad especificados por el usuario. En el árbol Página de la izquierda, haga clic en la capa Aeropuertos. En las propiedades de capa de la derecha, en Source, cambie Type a **SQL Query**. Para SQL Query, introduzca lo siguiente, que utiliza el operador SQL nativo de Oracle Database "dentro de la distancia".
    
        <copy>
        select a.*
          from EBA_SAMPLE_MAP_AIRPORTS a,
               EBA_SAMPLE_MAP_SIMPLE_STATES b
         where b.state_code= :P3_STATE
           and a.land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance='|| :P3_DISTANCE ||' unit=KM') = 'TRUE'
        </copy>
        
    
    Para los elementos de página que se van a enviar, introduzca la lista separada por comas **P3\_STATE,P3\_DISTANCE**.
    
    ![Consulta SQL espacial](images/add-spatial-analysis-15.png)
    
8.  La página ya está lista para su visualización. Haga clic en **Guardar** y, a continuación, en el botón verde **Ejecutar** situado en la parte superior derecha. Una vez presentada la página, para el estado, seleccione **Alabama**. El mapa muestra el estado y los aeropuertos seleccionados en un radio de 100 km (la distancia por defecto).
    
    ![Guardar y Ejecutar, página](images/add-spatial-analysis-16.png)
    
9.  Cambie el estado seleccionado a **Kansas**. Observe el mapa ahora que muestra el estado y los aeropuertos seleccionados con 100 km.
    
    ![Seleccionar Kansas](images/add-spatial-analysis-17.png)
    
10.  Aumente la distancia a 600 km y, a continuación, haga clic en Enter o Tab para enviar. Observe el mapa ahora muestra aeropuertos adicionales dentro de la distancia más grande.
    
    ![Aumente la distancia a 600 km](images/add-spatial-analysis-18.png)
    
11.  Por último, confirme que el envío de una distancia negativa da como resultado la ventana emergente Error que hemos configurado anteriormente.
    
    ![Alerta de distancia negativa](images/add-spatial-analysis-19.png)
    
    Como se muestra en la aplicación Mapas de ejemplo que instaló al principio de este taller, hay una gran cantidad de funciones adicionales que se pueden lograr con Map Regions y Spatial. Este taller ha presentado los conceptos básicos y esperamos que se haya despertado su interés y que aproveche la potencia de los mapas y los análisis espaciales en sus aplicaciones APEX.
    

## Más información

*   [Oracle Spatial.](https://www.oracle.com/database/spatial/)
*   [APEX](https://apex.oracle.com/)

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, Database Product Management, marzo de 2023