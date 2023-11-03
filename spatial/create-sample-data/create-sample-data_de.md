# Beispieldaten erstellen

## Einführung

In dieser Übung werden die Schritte zum Erstellen von räumlichen Beispieldaten in Oracle Database erläutert.

Geschätzte Laborzeit: 10 Minuten

### Ziele

In dieser Übung führen Sie folgende Schritte aus:

*   Informationen zum Spatial Data Management in Oracle Database
*   Spatial-Daten in Oracle Database aus gängigen Dateiformaten vorbereiten

### Voraussetzungen

*   Abschluss von Übung 2

### Informationen zu räumlichen Daten

Oracle Database speichert räumliche Daten (Punkte, Linien, Polygone) in einem nativen Datentyp namens SDO\_GEOMETRY. Oracle Database bietet außerdem einen nativen Spatial Index für leistungsstarke Spatial-Vorgänge. Dieser Spatial Index basiert auf räumlichen Metadaten, die für jede Tabelle und Geometriespalte mit räumlichen Daten eingegeben werden. Sobald räumliche Daten aufgefüllt und indiziert wurden, stehen robuste APIs zur Verfügung, um räumliche Analysen, Berechnungen und Verarbeitungen durchzuführen.

Der Typ SDO\_GEOMETRY hat das folgende allgemeine Format:

    SDO_GEOMETRY( 
     [geometry type],           --ID for point/line/polygon
     [coordinate system],       --ID of coordinate system
     [point coordinate],        --for points only
     [line/polygon info],       --for lines/polygons only
     [line/polygon coordinates] --for lines/polygons only
      )
    

Die häufigsten Geometrietypen sind 2-dimensional:

| ID | Typ |
| --- | --- |
| 2001 | Punkt |
| 2002 | Position |
| 2003 | Polygon |

Die gängigsten Koordinatensysteme sind:

| ID | Koordinatensystem |
| --- | --- |
| (4326) | Breite/Länge |
| (3857) | Welt-Mercator |

Beachten Sie bei der Verwendung von Breiten-/Längengrad, dass der Breitengrad die Y-Koordinate und der Längengrad die X-Koordinate ist. Da Koordinaten als X,Y-Paar aufgeführt sind, sind die Werte tatsächlich in der Reihenfolge Längengrad, Breitengrad.

Im Folgenden finden Sie eine Beispielpunktgeometrie mit Breiten-/Längengradkoordinaten:

    SDO_GEOMETRY( 
     2001,               --2D point
     4326,               --latitude/longitude
     SDO_POINT_TYPE(     
        -100.123, 20.456 --coordinate
        ),         
     NULL,               --for lines/polygons only
     NULL                --for lines/polygons only
      )
    

Im Folgenden finden Sie ein Beispiel für eine Polygongeometrie mit Breiten-/Längengradkoordinaten:

    SDO_GEOMETRY( 
     2003,                  --2D polygon
     4326,                  --latitude/longitude
     NULL,                  --for points only       
     SDO_ELEM_INFO_ARRAY(
          1, 1003, 1        --indicates simple exterior polygon
            ), 
     SDO_ORDINATE_ARRAY(   
        -98.789065,39.90973, -- coordinates
        -101.2522,39.639537,
        -99.84374,37.160316,
        -96.67987,35.460699,
        -94.21875,39.639537,
        -98.789025,39.90973
          )
        )
    );
    

### Ziele

In dieser Übung führen Sie folgende Schritte aus:

*   Tabellen mit einer Geometriespalte erstellen
*   Geometrien auffüllen
*   Spatial-Metadaten und -Indizes erstellen

### Voraussetzungen

Wie in der Workshop-Einführung beschrieben, benötigen Sie Zugriff auf einen Oracle Database- und SQL-Client. Wenn Sie diese nicht haben, gehen Sie zurück zu den Abschnitten im Oracle Cloud-Account, in Autonomous Database und in SQL Developer Web.

## Aufgabe 1: Tabellen mit Koordinaten erstellen

Zunächst erstellen wir Tabellen mit Breiten- und Längengradkoordinaten. Dies ist ein gemeinsamer Ausgangspunkt für die Erstellung von räumlichen Daten, z.B. Koordinaten aus GPS oder von Geocoding-Straßenadresse oder IP-Adresse.

Die Anweisungen und Screenshots beziehen sich auf SQL Developer Web. Für andere SQL-Clients gelten jedoch dieselben Schritte.

1.  Laden Sie das SQL-Skript [hier](files/create-sample-data.sql) herunter.
    
2.  Kopieren/einfügen/ausführen des Skripts in SQL Developer Web ![Alternativer Bildtext](images/run-script-1.png)
    
3.  Aktualisieren Sie die Liste, um die Tabellen BRANCHES und WAREHOUSES anzuzeigen
    
    ![Alternativer Bildtext](images/refresh-tables-1.png)
    

## Aufgabe 2: Geometrien aus Koordinaten erstellen

Geometrien können mit SQL gefüllt werden. Für Exathis-Fall können Sie die Koordinaten von Punktgeometrien basierend auf Breiten- und Längengradspalten angeben.

1.  Geometriespalten hinzufügen:
    
        <copy> 
        ALTER TABLE WAREHOUSES ADD (
         GEOMETRY SDO_GEOMETRY
        );
        
        ALTER TABLE BRANCHES ADD (
           GEOMETRY SDO_GEOMETRY
        );
        </copy>
        
2.  Geometriespalten auffüllen:
    
        <copy> 
        UPDATE WAREHOUSES
        SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
         UPDATE BRANCHES
         SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
        </copy>
        

## Aufgabe 3: Tabelle mit Polygon erstellen

Linien und Polygone können auf die gleiche Weise erstellt werden. Während eine Punktgeometrie eine Koordinate erfordert, erfordern Linien und Polygone alle Koordinaten, welche die Geometrie definieren. In diesem Fall erstellen wir eine Tabelle zum Speichern eines Polygons.

1.  Tabelle erstellen und Zeile einfügen
    
        <copy>
        CREATE TABLE COASTAL_ZONE (
            ZONE_ID   NUMBER,
            GEOMETRY  SDO_GEOMETRY
        );       
        
        INSERT INTO COASTAL_ZONE VALUES (
            1,
            SDO_GEOMETRY(
                2003, 4326, NULL, SDO_ELEM_INFO_ARRAY(
                    1, 1003, 1
                ), SDO_ORDINATE_ARRAY(
                    -93.719934, 30.210638,
                    -95.422592, 29.773714, 
                    -95.059698, 29.322204, 
                    -96.013892, 28.787021, 
                    -96.660964, 28.925638, 
                    -97.528688, 28.042050, 
                    -97.858501, 27.447461, 
                    -97.497364, 25.880056, 
                    -96.977826, 25.969716, 
                    -97.211445, 27.054605, 
                    -96.870226, 27.816077, 
                    -93.794290, 29.535729, 
                    -93.719934, 30.210638
                )
            )
        );
        </copy>
        
2.  Aktualisieren Sie die Tabellenliste, um die Tabelle COASTAL\_ZONE anzuzeigen. ![Alternativer Bildtext](images/refresh-tables-2.png)
    

## Aufgabe 4: Spatial-Metadaten und -Indizes hinzufügen

Oracle Database bietet einen nativen Spatial Index für leistungsstarke Spatial-Vorgänge. Unsere Beispieldaten sind so klein, dass ein Spatial Index nicht wirklich benötigt wird. Wir führen jedoch die folgenden Schritte aus, da sie für typische Produktionsdatenmengen wichtig sind. Ein Spatial Index erfordert eine Metadatenzeile für die indizierte Geometrie. Diese Metadaten und dann die Spatial Indexes werden erstellt.

1.  Spatial-Metadaten hinzufügen:
    
        <copy> 
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'WAREHOUSES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'BRANCHES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'COASTAL_ZONE',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        </copy>
        
2.  Spatial Indexes erstellen:
    
        <copy> 
        CREATE INDEX WAREHOUSES_SIDX ON
            WAREHOUSES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX BRANCHES_SIDX ON
            BRANCHES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX COASTAL_ZONE_SIDX ON
            COASTAL_ZONE (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
         </copy>
        
    
    Aktualisieren Sie die Tabellenliste, nachdem die Indizes erstellt wurden. Es werden 3 Tabellen angezeigt, deren Namen mit MDRT\_ beginnen. Dies sind Artefakte der Spatial Indexes, die von Oracle Database automatisch verwaltet werden. Sie sollten diese Tabellen niemals manuell bearbeiten. ![Alternativer Bildtext](images/refresh-tables-3.png)
    
    Unsere Beispieldaten sind jetzt für räumliche Abfragen vorbereitet und bereit.
    
    Sie können jetzt mit der nächsten Übung fortfahren.
    
    Wenn Sie diese Übung rückgängig machen und die erstellten Elemente entfernen müssen, führen Sie Folgendes aus:
    
         DROP TABLE BRANCHES;   
         DROP TABLE WAREHOUSES;
         DROP TABLE COASTAL_ZONE;
         DELETE FROM USER_SDO_GEOM_METADATA;
         COMMIT;
        

## Weitere Informationen

*   \[Räumliches Produktportal\] (https://oracle.com/goto/spatial)
*   [Räumliche Dokumentation](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Spatial-Blogs](https://blogs.oracle.com/oraclespatial/)

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - Kamryn Vinson, November 2020