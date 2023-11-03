# Limpiar

## Introducción

Puede limpiar el entorno del taller restableciendo Autonomous Database al estado anterior al taller.

Tiempo de laboratorio estimado: 2 minutos

### Objetivos

*   Restablecimiento de Autonomous Database al estado previo al taller

### Requisitos

*   Instancia de Autonomous Database activa

## Tarea 1: Restablecimiento de Autonomous Database al estado anterior al taller

1.  Ejecute lo siguiente para eliminar todos los artefactos de base de datos creados en este taller.
    
        <copy>
        import oracledb
        my_pwd = open('./my-pwd.txt','r').readline().strip()
        my_dsn = open('./my-dsn.txt','r').readline().strip()
        connection = oracledb.connect(user="admin", password=my_pwd, dsn=my_dsn)
        cursor = connection.cursor()
        cursor.execute("drop table transactions")
        cursor.execute("drop table locations")
        cursor.execute("drop table transaction_labels")
        cursor.execute("drop function lonlat_to_proj_geom")
        cursor.execute("delete from user_sdo_geom_metadata")
        connection.commit()
        </copy>
        

## Reconocimientos

*   **Autor**: David Lapp, Database Product Management, Oracle
*   **Última actualización por/fecha**: David Lapp, agosto de 2023