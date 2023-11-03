# Bereinigen

## Einführung

Sie können Ihre Workshopumgebung bereinigen, indem Sie Autonomous Database auf den Status vor dem Workshop zurücksetzen.

Geschätzte Laborzeit: 2 Minuten

### Ziele

*   Autonomous Database auf Pre-Workshop-Status zurücksetzen

### Voraussetzungen

*   Aktive Autonomous Database-Instanz

## Aufgabe 1: Autonomous Database auf Pre-Workshop-Status zurücksetzen

1.  Führen Sie den folgenden Befehl aus, um alle in diesem Workshop erstellten Datenbankartefakte zu entfernen.
    
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
        

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, August 2023