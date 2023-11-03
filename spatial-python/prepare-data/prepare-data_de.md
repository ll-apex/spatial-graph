# Daten vorbereiten

## Einführung

In dieser Übung werden fiktive Finanztransaktionsdaten in Ihre Autonomous Database geladen und für räumliche und zeitliche ("spatiotemporale") Analysen konfiguriert.

Geschätzte Laborzeit: 10 Minuten

### Ziele

*   Finanztransaktionsdaten in Autonomous Database laden
*   Daten für raumzeitliche Analysen konfigurieren

### Voraussetzungen

*   Abschluss der Übung 4: Verbindung zu Autonomous Database von Python herstellen

## Aufgabe 1: Datendateien hochladen

1.  Verwenden Sie die folgenden Links, um die Datendateien herunterzuladen:

*   [locations.csv](./data/locations.csv)
*   [transactions.csv](./data/transactions.csv)

2.  Klicken Sie auf das Symbol **Hochladen**, um die Datendateien zu laden. ![Daten hochladen](images/prepare-data-01.png)
    
3.  Doppelklicken Sie im linken Bereich auf locations.csv und transactions.csv, um eine Vorschau der Datendateien in neuen Registerkarten anzuzeigen.
    
    ![Vorschau von Dateien anzeigen](images/prepare-data-02.png)
    

Beachten Sie, dass locations.csv eine Zeile pro GA-Standort hat und Transaktionen eine Zeile pro Finanztransaktion aufweisen. Schließen Sie dann Tabs mit der Datenvorschau, und kehren Sie zu Ihrem Notizbuch zurück.

## Aufgabe 2: Tabellen erstellen und laden

1.  Fügen Sie in der nächsten Zelle Ihres Notizbuchs die folgende Anweisung ein, und klicken Sie auf die Schaltfläche **Ausführen**. Dadurch wird die Tabelle für die Standortdaten erstellt.
    
        <copy>
        # Create table for locations data
        cursor.execute("""
         CREATE TABLE locations (
                   location_id INTEGER,
                   owner VARCHAR2(100),  
                   lon NUMBER,
                   lat NUMBER)""")
        </copy>
        
    
    ![Daten laden](images/prepare-data-04.png)
    
2.  Führen Sie den folgenden Befehl aus, um die Standortdaten zu laden.
    
        <copy>
        # Load the locations data
        import csv
        BATCH_SIZE = 1000
        with connection.cursor() as cursor:
            with open('locations.csv', 'r') as csv_file:
                csv_reader = csv.reader(csv_file, delimiter=',')
                #skip header
                next(csv_reader)
                #load data
                sql = "INSERT INTO locations VALUES (:1, :2, :3, :4)"
                data = []
                for line in csv_reader:
                    data.append((line[0], line[1], line[2], line[3]))
                    if len(data) % BATCH_SIZE == 0:
                        cursor.executemany(sql, data)
                        data = []
                if data:
                    cursor.executemany(sql, data)
                connection.commit()
        </copy>
        
    
    ![Daten laden](images/prepare-data-05.png)
    
3.  Führen Sie den folgenden Befehl aus, um eine Vorschau der Standortdaten anzuzeigen, die jeweils eine Zeile für jeden Geldautomatenstandort enthält, einschließlich Koordinaten und einer eindeutigen Standort-ID.
    
        <copy>
        # Preview locations data
        cursor = connection.cursor()
        cursor.execute("SELECT * FROM locations")
        for row in cursor.fetchmany(size=10):
            print(row)
        </copy>
        
    
    ![Datenvorschau](images/prepare-data-06.png)
    
4.  Fügen Sie in der nächsten Zelle die folgende Anweisung ein, und klicken Sie auf die Schaltfläche **Ausführen**. Dadurch wird die Tabelle für die Transaktionsdaten erstellt.
    
        <copy>
        # Create table for transactions data
        cursor.execute("""
           CREATE TABLE transactions (
                          trans_id INTEGER,
                          location_id INTEGER,
                          trans_date DATE,
                          cust_id INTEGER)""")
        </copy>
        
    
    ![Tabelle erstellen](images/prepare-data-07.png)
    
5.  Führen Sie den folgenden Befehl aus, um die Transaktionsdaten zu laden.
    
        <copy>
        # Load the transactions data
        BATCH_SIZE = 1000
        with connection.cursor() as cursor:
            with open('transactions.csv', 'r') as csv_file:
                csv_reader = csv.reader(csv_file, delimiter=',')
                #skip header
                next(csv_reader)
                #load data
                sql = "INSERT INTO transactions VALUES (:1, :2, TO_DATE(:3,'YYYY-MM-DD:HH24:MI:SS'), :4)"
                data = []
                for line in csv_reader:
                    data.append((line[0], line[1], line[2], line[3]))
                    if len(data) % BATCH_SIZE == 0:
                        cursor.executemany(sql, data)
                        data = []
                if data:
                    cursor.executemany(sql, data)
                connection.commit()
        </copy>
        
    
    ![Daten laden](images/prepare-data-08.png)
    
6.  Führen Sie den folgenden Befehl aus, um eine Vorschau der Transaktionsdaten anzuzeigen, die eine Zeile für jede Transaktion enthält, einschließlich Daten und Standort-ID.
    
        <copy>
        # Preview transactions data
        cursor = connection.cursor()
        cursor.execute("SELECT * FROM transactions")
        for row in cursor.fetchmany(size=10):
            print(row)
        </copy>
        
    
    ![Datenvorschau](images/prepare-data-09.png)
    
7.  Führen Sie die folgenden Schritte aus, um die eindeutigen Kunden-IDs aufzulisten.
    
        <copy>
        # Customer ID's
        cursor = connection.cursor()
        cursor.execute("SELECT DISTINCT cust_id FROM transactions ORDER BY cust_id")
        for row in cursor.fetchall():
            print(row[0])
        </copy>
        
    
    ![Listen-IDs](images/prepare-data-09a.png)
    

## Aufgabe 3: Epochendatum hinzufügen

Zeitliche Berechnungen sind ein wichtiger Bestandteil dieses Workshops und werden am besten mit einer ganzzahligen Darstellung von Datum und Uhrzeit durchgeführt. Diese Ganzzahldarstellung wird allgemein als Epochenzeit oder genauer als UNIX-Zeit bezeichnet. In dieser Aufgabe fügen Sie Epochenzeit für alle Transaktionen hinzu.

1.  Führen Sie den folgenden Befehl aus, um eine Spalte für das Epochendatum hinzuzufügen und zu füllen.
    
        <copy>
        # add column for epoch date
        cursor.execute("ALTER TABLE transactions ADD (trans_epoch_date integer)")
        </copy>
        
    
        <copy>
        # add column for epoch date
        cursor.execute("""UPDATE transactions
                          SET trans_epoch_date = (trans_date - date'1970-01-01') * 86400""")
        connection.commit()
        </copy>
        
    
    ![Epoch-Datum hinzufügen](images/prepare-data-10.png)
    
2.  Führen Sie den folgenden Befehl aus, um erneut eine Vorschau der Transaktionsdaten anzuzeigen. Beachten Sie, dass die Spalte für das Epochendatum hinzugefügt wird.
    
        <copy>
        # Preview transactions data
        cursor.execute("SELECT * FROM transactions")
        for row in cursor.fetchmany(size=10):
            print(row)
        </copy>
        
    
    ![Vorschau Epoch-Datum](images/prepare-data-11.png)
    

## Aufgabe 4: Daten für räumliche Vorgänge konfigurieren

Räumliche Berechnungen sind ein weiterer wichtiger Bestandteil dieses Workshops. In dieser Aufgabe konfigurieren Sie die Standortdaten so, dass sie die räumlichen Features von Autonomous Database nutzen. Die Standorttabelle enthält Längen-/Breitengradkoordinaten. Eine Möglichkeit besteht darin, eine neue Spalte mit dem nativen räumlichen Datentyp zu erstellen und zu füllen. Das würde zwar perfekt funktionieren, aber es gibt eine weitere Option, die ein Mainstream-Feature von Oracle Database nutzt, das als funktionale Indexierung bezeichnet wird. Dieser Ansatz ermöglicht alle Funktionen, die mit dem Erstellen einer neuen räumlichen Spalte verbunden sind, ohne jedoch die Spalte erstellen zu müssen. Stattdessen erstellen Sie eine Datenbankfunktion, die Koordinaten in ein räumliches Datenelement konvertiert und dann einen Index für diese Funktion erstellt. Nachdem die Funktion und der Index erstellt wurden, verhalten sich alle räumlichen Operationen so, als ob eine neue räumliche Spalte erstellt worden wäre. Dies ist zwar für das kleine Datenvolumen in diesem Workshop nicht unerlässlich, aber der Ansatz ist von großem Nutzen für große Systeme, bei denen der Aufwand für das Hinzufügen einer Spalte erheblich ist.

1.  Führen Sie den folgenden Befehl aus, um eine Funktion zu erstellen, die Längen-/Breitengradkoordinaten in den nativen räumlichen Datentyp von Oracle konvertiert (d.h. SDO\_GEOMETRY, als "Geometrie" bezeichnet). Die Funktion konvertiert nicht nur Koordinaten in den nativen räumlichen Typ, sondern konvertiert auch die Koordinaten von Längen-/Breitengrad in ein Koordinatensystem namens "Weltmercator". Dies ist das Koordinatensystem, das von Python-Librarys erwartet wird, die in nachfolgenden Übungen verwendet werden. Daher ist es praktisch, diese Konvertierung in dieser Funktion auszuführen.
    
        <copy>
        # Create function to return lon/lat coordinates as a geometry.
        cursor.execute("""
         CREATE OR REPLACE FUNCTION lonlat_to_proj_geom (longitude IN NUMBER, latitude IN NUMBER)
         RETURN SDO_GEOMETRY DETERMINISTIC IS
         BEGIN
           IF latitude IS NULL OR longitude IS NULL
           OR latitude NOT BETWEEN -90 AND 90
           OR longitude NOT BETWEEN -180 AND 180
           THEN
             RETURN NULL;
           ELSE
              RETURN sdo_cs.transform(
                SDO_GEOMETRY(2001, 4326,
                             sdo_point_type(longitude, latitude, NULL),NULL, NULL),
                3857);
           END IF;
        END;""")
        </copy>
        
    
    ![Funktion erstellen](images/prepare-data-13.png)
    
2.  Die Abfrage von Geometrien und Geometrien, die in Zeichenfolgendarstellungen konvertiert werden, umfasst "Große Objekte" oder "LOBs". Wenden Sie die folgende Einstellung auf python-oracledb an, damit LOBs direkt abgerufen werden, anstatt einen LOB-Positionsanzeiger abzurufen und dann den LOB-Inhalt in einer zweiten Roundtrip abzurufen.
    
        <copy>
        # return LOBs directly as strings or bytes
        oracledb.defaults.fetch_lobs = False  
        </copy>
        
    
    ![LOB-Option festlegen](images/fetch-lobs.png)
    
3.  Führen Sie den folgenden Befehl aus, um die Funktion zu testen.
    
        <copy>
        # test the function
        cursor.execute("""
         with x as (
            SELECT location_id, lonlat_to_proj_geom(lon,lat) as geom FROM locations)
         SELECT location_id, geom, (geom).get_wkt()
         FROM x
         """)
        for row in cursor.fetchone():
            print(row)
        </copy>
        
    
    ![Funktion testen](images/prepare-data-14.png)
    
4.  Räumliche Abfragen basieren auf einem Spatial Index für eine optimale Performance. Ein Spatial Index kann nur für Daten mit einheitlicher Dimensionalität (d.h. 2D oder 3D) und Koordinatensystem erstellt werden. Bevor Sie einen Spatial Index erstellen, müssen Sie eine Zeile mit Metadaten einfügen, die diese Eigenschaften beschreibt, damit die Geometrie indexiert werden kann. Dazu gehören der Tabellenname, der Name der Geometriespalte (oder in diesem Fall eine Funktion, die Geometrie zurückgibt), die Dimensionalität und ein Koordinatensystemcode. Beim Erstellen eines Spatial Index werden die Daten zunächst geprüft, ob sie den Metadaten entsprechen. Die räumliche Indizierung wird nur erfolgreich abgeschlossen, wenn die Daten den Metadaten entsprechen. Führen Sie den folgenden Befehl aus, um räumliche Metadaten für die Standortgeometrie zu erstellen.
    
        <copy>
        cursor.execute("""
         INSERT INTO user_sdo_geom_metadata VALUES (
            'LOCATIONS', 'ADMIN.LONLAT_TO_PROJ_GEOM(LON,LAT)',
             SDO_DIM_ARRAY(SDO_DIM_ELEMENT('LON', 0, 0, 0.05),
                           SDO_DIM_ELEMENT('LAT', 0, 0, 0.05)),
             3857)
                    """)
        </copy>
        
    
    ![Metadaten einfügen](images/prepare-data-15.png)
    
5.  Führen Sie den folgenden Befehl aus, um einen Spatial Index für die Standortgeometrie zu erstellen.
    
        <copy>
        cursor.execute("""
         CREATE INDEX locations_sidx
         ON locations(LONLAT_TO_PROJ_GEOM(LON,LAT))
         INDEXTYPE IS mdsys.spatial_index_v2
                    """)
        </copy>
        
    
    ![Index erstellen](images/prepare-data-16.png)
    
6.  Um den Spatial Index zu prüfen, führen Sie die folgende Spatial-Beispielabfrage aus. Diese Abfrage gibt die 5 nächsten Elemente aus der Tabelle **locations** in einen Längengrad, eine Breitengradkoordinate sowie die Entfernungen zurück. Diese Abfrage wird als "naheste Nachbar"-Abfrage bezeichnet und verwendet den Operator **sdo\_nn( )**, der den Spatial Index verwendet. Weitere Informationen zu Abfragen am nächsten Nachbarn finden Sie in der [Dokumentation](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl/spatial-operators-reference.html#GUID-41E6B1FA-1A03-480B-996F-830E8566661D).
    
        <copy>
        cursor.execute("""
         SELECT location_id, round(sdo_nn_distance(1), 2) FROM locations
         WHERE sdo_nn(
           LONLAT_TO_PROJ_GEOM(LON,LAT),
           LONLAT_TO_PROJ_GEOM( -97.6, 30.3),
           'sdo_num_res=5 unit=mile', 1) = 'TRUE' """)
        for row in cursor.fetchmany():
            print(row)  
        </copy>
        
    
    ![Spatial Query ausführen](images/prepare-data-18.png)
    

Sie können jetzt **mit der nächsten Übung fortfahren**.

## Weitere Informationen

*   Einzelheiten zur UNIX-Zeit finden Sie unter [https://en.wikipedia.org/wiki/Unix\_time](https://en.wikipedia.org/wiki/Unix_time)
*   Einzelheiten zur funktionsbasierten räumlichen Indexierung finden Sie in der [Dokumentation](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl/extending-spatial-indexing.html#GUID-CFB6B6DB-4B97-43D1-86A1-21C1BA853089).

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Mitwirkende** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Zuletzt aktualisiert am/um** - David Lapp, August 2023