# Graph Studio: carga de datos de archivos CSV en tablas

## Introducción

En este laboratorio, cargará dos archivos CSV en las tablas correspondientes mediante la interfaz de Database Actions en la instancia de Oracle Autonomous Data Warehouse u Oracle Autonomous Transaction Processing.

Tiempo estimado: 10 minutos.

Vea el siguiente video para ver un breve recorrido por el laboratorio.

[](youtube:wkKKO-RO0lA)

### Objetivos

Información sobre cómo

*   Cargar archivos CSV en una instancia de Autonomous Database mediante Database Actions

### Requisitos

*   El siguiente laboratorio requiere una cuenta de Oracle Autonomous Database.
*   Se asume que existe un usuario habilitado para gráficos y acceso web. Es decir, existe un usuario de base de datos con los roles y privilegios correctos y ese usuario puede conectarse a Database Actions.

## Tarea 1: Conexión a Database Actions para la instancia de Autonomous Database

1.  Abra la página de detalles del servicio de su instancia de Autonomous Database en la consola de Oracle Cloud.
    
    ![El texto alternativo no está disponible para esta imagen](images/open-database-actions.png " ")
    
2.  Haga clic en **Database Actions** para abrirlo.
    

## Tarea 2: Conexión como usuario activado para gráficos

1.  Conéctese como usuario de gráfico (por ejemplo, `GRAPHUSER`) para la instancia de Autonomous Database.
    
    ![El texto alternativo no está disponible para esta imagen](./images/db-actions-graphuser-login.png " ")
    
    > **Nota:** _Si es necesario, haga lo siguiente para crear el usuario con los roles y privilegios adecuados_:
    
    *   Conexión a Database Actions como usuario **ADMIN** para su instancia de Autonomous Database
    *   Seleccione **Administración** y, a continuación, **Usuarios de Base de Datos** en el menú de navegación
    *   Haga clic en **Crear usuario**.
    *   Activar los botones **Acceso web** y **Gráfico**

## Tarea 3: Descargar los conjuntos de datos de ejemplo de ObjectStore

1.  Copie y pegue la URL en el explorador para el archivo zip, es decir,
    
        <copy>
        https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
    
    O bien, utilice `wget` o `curl` para descargar los datos de ejemplo en el equipo.  
    Una solicitud `curl` de ejemplo que puede copiar y pegar es:
    
        <copy>
        curl -G -o acct-txn-data.zip https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
2.  **Descomprima** el archivo en un directorio local, como ~/descargas.
    

## Tarea 4: Carga mediante la carga de datos de Database Actions

1.  Haga clic en la tarjeta **DATA LOAD** (Cargar datos).
    
    ![El texto alternativo no está disponible para esta imagen](images/db-actions-dataload-card.png " ")
    
    A continuación, especifique la ubicación de los datos. Es decir, asegúrese de que las tarjetas **LOAD DATA** y **LOCAL FILE** tengan una marca de verificación. Haga clic en **Siguiente**.
    
    ![El texto alternativo no está disponible para esta imagen](./images/db-actions-dataload-location.png)
    
2.  Haga clic en **Seleccionar archivos**.
    
    ![El texto alternativo no está disponible para esta imagen](images/db-action-dataload-file-browser.png " ")
    
    Navegue a la carpeta correcta (por ejemplo, ~/downloads/random-acct-data) y seleccione los archivos `bank_accounts.csv` y `bank_txns.csv`.
    
    ![El texto alternativo no está disponible para esta imagen](./images/db-actions-dataload-choose-files.png " ")
    
3.  Verifique que se hayan seleccionado los archivos correctos y, a continuación, haga clic en el icono **Ejecutar**. ![El texto alternativo no está disponible para esta imagen](./images/db-actions-dataload-click-run.png " ")
    
4.  Confirme que desea el trabajo de carga de datos.
    
    ![El texto alternativo no está disponible para esta imagen](./images/db-actions-dataload-confirm-run.png " ")
    
5.  Una vez cargados los archivos
    
    ![El texto alternativo no está disponible para esta imagen](./images/dbactions-dataload-files-loaded.png " ")
    
    Haga clic en **Listo** para salir.
    
    ![El texto alternativo no está disponible para esta imagen](images/dbactions-click-done.png " ")
    
6.  Ahora abra la hoja de trabajo de **SQL**. ![El texto alternativo no está disponible para esta imagen](./images/db-actions-choose-sql-card.png " ")
    
7.  Navegue a la carpeta correcta (por ejemplo, ~/descargas), seleccione el archivo `fixup.sql` y arrástrelo a la hoja de trabajo de SQL.
    
    ![El texto alternativo no está disponible para esta imagen](./images/db-actions-drag-drop-fixup-sql.png " ")
    
    Sin embargo, si prefiere copiar y pegar, el contenido de `fixup.sql` es:
    
        <copy>
        alter table bank_accounts add primary key (acct_id);
        
        alter table bank_txns add txn_id number;
        update bank_txns set txn_id = rownum;
        commit;
        
        alter table bank_txns add primary key (txn_id);
        alter table bank_txns modify from_acct_id references bank_accounts (acct_id);
        alter table bank_txns modify to_acct_id references bank_accounts (acct_id);
        
        desc bank_txns;
        
        select * from USER_CONS_COLUMNS where table_name in ('BANK_ACCOUNTS', 'BANK_TXNS');
        </copy>      
        
    
    En este documento:
    
    *   Agrega una restricción de clave primaria a la tabla `bank_accounts`
    *   Agrega una columna (`txn_id`) a la tabla `bank_txns`
    *   Define un valor para `txn_id` y confirma la transacción
    *   Agrega una restricción de clave primaria a la tabla `bank_txns`
    *   Agrega una restricción de clave ajena a la tabla `bank_txns` especificando que `from_acct_id` hace referencia a `bank_accounts.acct_id`
    *   Agrega una segunda restricción de clave ajena a la tabla `bank_txns` especificando que `to_acct_id` hace referencia a `bank_accounts.acct_id`
    *   Ayuda a verificar que la adición de una columna `txn_id` y las restricciones
8.  Ejecute el script `fixup.sql` en la hoja de trabajo de SQL.  
    ![El texto alternativo no está disponible para esta imagen](./images/db-actions-sql-execute-fixup.png " ")
    
9.  La salida del script debe tener el siguiente aspecto:
    
    ![El texto alternativo no está disponible para esta imagen](./images/db-actions-sql-script-output.png " ")
    
    **Continúe con el siguiente ejercicio práctico** para crear un gráfico a partir de estas tablas.
    

## Reconocimientos

*   **Autor**: Jayant Sharma, gestión de productos
*   **Contribuyentes**: Jayant Sharma, gestión de productos
*   **Última actualización por/fecha**: Jayant Sharma, gestión de productos, febrero de 2022