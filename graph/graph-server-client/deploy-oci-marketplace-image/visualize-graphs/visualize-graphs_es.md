# Visualización del gráfico

## Introducción

Los resultados de los análisis realizados en las prácticas anteriores se pueden visualizar fácilmente mediante la función Visualización de gráficos.

Tiempo estimado: 5 minutos

En el siguiente vídeo se proporciona una visión general del componente Visualización de gráficos (= GraphViz).

[YouTube](youtube:zfefKdNfAY4)

### Objetivos

*   Descubra cómo ejecutar consultas de gráficos PGQL y visualizar los resultados.

### Requisitos

*   Se crea y publica el gráfico
*   El servidor de gráficos (con GraphViz) está activo y en ejecución

## Tarea 1: Conéctese a GraphViz

Abra GraphViz en **`https://<public_ip_for_compute>:7007/ui`** mediante un explorador web. Sustituya **`<public_ip_for_compute>`** por el de la instancia informática de Graph Server.

Dado que la imagen de marketplace se distribuye con un certificado SSL autofirmado, debe cambiarlo para su propio certificado en uso de producción. Mientras tanto, los navegadores web deben mostrar advertencias, mientras entendemos que es seguro.

Si utiliza **Chrome**, escriba **thisisunsafe** en la ventana de advertencia para pasar a la pantalla GraphViz.

![cromo de inicio de sesión](images/login-chrome.jpg)

Con **Firefox**, haga clic en **Avanzado** y, a continuación, en **Aceptar el riesgo y continuar**.

![inicio de sesión-firefox](images/login-firefox.jpg)

Debería ver una pantalla similar a la siguiente. Introduzca el nombre de usuario (**customer\_360**) y la contraseña y, a continuación, haga clic en Enviar. **Graph Server** es el valor por defecto en Advanced Options, por lo que no es necesario cambiarlo.

![conexión](images/login.jpg)

## Tarea 2: Modificar consulta

Modifique la consulta para obtener las primeras 5 filas, es decir, cambie **LIMIT 100** a **LIMIT 5** y haga clic en Run.

Debería ver un gráfico similar al de la siguiente captura de pantalla.

![elementos show-5](images/show-5-elements.jpg)

## Tarea 3: Agregar resaltados

Ahora vamos a añadir algunas etiquetas y otro contexto visual. Estos se conocen como aspectos destacados. Haga clic [aquí](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/highlights.json.zip) para descargar un archivo zip, highlights.json.zip. Descomprima este archivo y observe dónde se descomprime.

Haga clic en el botón Load (Cargar) en **Settings** (Configuración) (en el lado derecho de la pantalla). Vaya a la carpeta adecuada, elija el archivo y haga clic en Open para cargarlo.

![puntos destacados-1](images/highlights-1.png)

El gráfico ahora debería verse como

![puntos destacados-2](images/highlights-2.png)

## Tarea 4: Coincidencia de patrones con PGQL

1.  A continuación, vamos a ejecutar algunas consultas PGQL.
    
    El sitio [pgql-lang.org](http://pgql-lang.org) y la [especificación](http://pgql-lang.org/spec/1.4) son las mejores referencias para obtener detalles y ejemplos. Sin embargo, para los fines de este laboratorio, aquí hay conceptos básicos mínimos.
    
    La estructura general de una consulta PGQL es:
    
        <copy>
        SELECT <select_list>
        FROM MATCH <graph_pattern> ON <graph_name>
        WHERE <condition>
        </copy>
        
    
    PGQL proporciona una construcción específica conocida como cláusula **MATCH** para los patrones de gráficos coincidentes. Un patrón de gráfico coincide con vértices y bordes que cumplen las condiciones y restricciones proporcionadas.
    
    *   **(v)** indica una variable de vértice **v**
    *   **\-** indica un borde no dirigido, como en (origen)-(destino)
    *   **\->** un borde saliente del origen al destino
    *   **<**: un borde entrante del destino al origen
    *   **\[e\]** indica una variable de borde **e**
    
    Además, omita **graph\_name** aquí, ya que está seleccionado en la interfaz de usuario GraphViz.
    
2.  Vamos a encontrar cuentas que han tenido una transferencia saliente y entrante de más de 500 en el mismo día.
    
    La consulta PGQL para esto es:
    
        <copy>
        SELECT *
        FROM MATCH (a)-[t1:transfer]->(a1)
           , MATCH (a2)-[t2:transfer]->(a)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
        </copy>
        
    
    En la primera cláusula **MATCH** anterior, **(a)** indica el vértice de origen y **(a1)** el destino, mientras que **\[t1:transfer\]** es el borde que los conecta. **:transfer** especifica que el borde **t1** tiene la etiqueta **TRANSFER**. La coma (,) entre los dos patrones es una condición AND.
    
3.  Copie y pegue la consulta en el cuadro de entrada de texto PGQL Graph Query de la aplicación GraphViz. Haga clic en Run.
    
    El resultado debe verse como se muestra a continuación. En la configuración resaltada, las cuentas que comienzan con **xxx-yyy-** se muestran en rojo (= cuentas del banco), mientras que **xxx-zzz-** se muestran en naranja (= cuentas de otro banco).
    
    ![transferencias del mismo día](images/same-day-transfers.jpg)
    
4.  La siguiente consulta busca patrones de transferencias desde y hacia las mismas dos cuentas, es decir, desde a1->a2 y hacia atrás a2->a1.
    
    La consulta PGQL para esto es:
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
        </copy>
        
5.  Copie y pegue la consulta en el cuadro de entrada de texto PGQL Graph Query de la aplicación GraphViz. Haga clic en Run.
    
    El resultado debe verse como se muestra a continuación.
    
    ![Ciclo 2 - Talleres](images/cycle-2-hops.jpg)
    
6.  Vamos a agregar una cuenta más a esa consulta para encontrar un patrón de transferencia circular entre 3 cuentas.
    
    La consulta PGQL se convierte en:
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
        </copy>
        
7.  Copie y pegue la consulta en el cuadro de entrada de texto PGQL Graph Query de la aplicación GraphViz. Haga clic en Run.
    
    El resultado debe verse como se muestra a continuación.
    
    ![Ciclo 3 - Talleres](images/cycle-3-hops.jpg)
    

## Reconocimientos

*   **Autor**: Jayant Sharma
*   **Contribuyentes** - Arabella Yao, Jenny Tsai
*   **Última actualización por/fecha**: Ryota Yamanaka, marzo de 2023