# GeoJSON zurückgeben

## Einführung

GeoJSON ist das bevorzugte Format für die Entwicklerintegration räumlicher Daten. Praktisch alle räumlichen und Mapping-Clientbibliotheken belegen GeoJSON. Daher ist es wichtig, Inhalte und Ergebnisse aus Spatial als GeoJSON zurückzugeben. Eine Erläuterung zu GeoJSON finden Sie unter **Übung 3 - Einführung**. In dieser Übung generieren Sie GeoJSON-Dokumente aus Tabellen mit Geometrien. In der Praxis besteht der Wert der Generierung von GeoJSON in ADB darin, GeoJSON an verschiedene Clients zurückzugeben und dann den Inhalt aus ihrem Framework bereitzustellen. Beispiel: SQL und PL/SQL, die GeoJSON zurückgeben, können von Oracle REST Data Services (ORDS) verwendet werden, um standortbasierte REST-APIs zu veröffentlichen, die GeoJSON-Dokumente zurückgeben, und Oracle Data Science, um sie mit gängigen räumlichen Open-Source-ML-Librarys zu kombinieren, die GeoJSON nativ unterstützen.

Geschätzte Zeit: 15 Minuten

Sehen Sie sich das Video unten an, um einen schnellen Durchgang des Labors zu erhalten. [Spatial-Daten vorbereiten](videohub:1_bj22bt29)

### Ziele

In dieser Übung führen Sie folgende Schritte aus:

*   Entdecken Sie native JSON-Übergabe in Oracle Autonomous Database
*   Konvertieren von Tabellen mit Geometrien in GeoJSON-Dokumente zur Unterstützung der Entwicklerintegration

### Voraussetzungen

*   Abschluss von Übung 3: Räumliche Daten vorbereiten

## Aufgabe 1: GeoJSON-Dokument aus Abfrageergebnissen erstellen

1.  Geben Sie zunächst eine Tornado-Pfadgeometrie im Format GeoJSON zurück.
    
        <copy> 
        SELECT
            SDO_UTIL.TO_GEOJSON(GEOMETRY)
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON zurückgeben](images/return-geojson-01.png)
    
2.  Verwenden Sie als Nächstes die Funktion JSON\_ARRAYAGG( ), um Zeilen mit GeoJSON-Geometrien nach Bedarf in ein Array zu konvertieren, um das Dokument GeoJSON zu erstellen. Beachten Sie das Argument **RETURNING CLOB**, das erforderlich ist, da Geometrien mit vielen Koordinaten (wie komplexe Polygone) zu sehr langen Zeichenfolgen führen können. Bewegen Sie den Mauszeiger über das Ergebnis, um das JSON-Array anzuzeigen.
    
        <copy> 
        SELECT
            JSON_ARRAYAGG(
                SDO_UTIL.TO_GEOJSON(GEOMETRY) 
                FORMAT JSON RETURNING CLOB )
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON zurückgeben](images/return-geojson-02.png)
    
3.  Das Feature-Array muss sowohl Geometrien als auch Eigenschaften enthalten. Führen Sie die folgende Abfrage aus, um Elemente des Featurearrays zu erstellen. Zeigen Sie mit der Maus auf das Ergebnis, um das JSON-Array jetzt mit Eigenschaften anzuzeigen.
    
        <copy> 
        SELECT
            '{"type": "Feature", "properties": {'
            || '"key":"'|| KEY
            ||'","yr":"'|| YR
            ||'","loss":"'|| LOSS
            ||'"}, "geometry":'|| SDO_UTIL.TO_GEOJSON(GEOMETRY)
            ||'}' AS features
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON zurückgeben](images/return-geojson-03.png)
    
4.  Verwenden Sie JSON\_ARRAYAGG( ), um die vorherigen Ergebnisse in einem Array zu kompilieren. Dies ist nun das eigentliche Features-Array. Zeigen Sie mit der Maus auf das Ergebnis, um ein Popup mit dem Ergebnis anzuzeigen.
    
        <copy> 
        SELECT
            JSON_ARRAYAGG( 
                '{"type": "Feature", "properties": {'
                || '"key":"'|| KEY
                ||'","yr":"'|| YR
                ||'","loss":"'|| LOSS
                ||'"}, "geometry":'|| SDO_UTIL.TO_GEOJSON(GEOMETRY)
                ||'}' 
                FORMAT JSON RETURNING CLOB)   
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON zurückgeben](images/return-geojson-04.png)
    
5.  Um die Erstellung eines GeoJSON-Dokuments abzuschließen, nehmen Sie die Schlüssel der obersten Ebene **type** und **features** sowie eine schließende geschweifte Klammer auf. Dadurch wird nun ein vollständiges GeoJSON-Dokument zurückgegeben. Zeigen Sie mit der Maus auf das Ergebnis, um ein Popup mit dem Ergebnis anzuzeigen.
    
        <copy> 
        SELECT
            '{"type": "FeatureCollection", "features":'
            || JSON_ARRAYAGG( 
                '{"type": "Feature", "properties": {'
                || '"key":"'|| KEY
                ||'","yr":"'|| YR
                ||'","loss":"'|| LOSS
                ||'"}, "geometry":'|| SDO_UTIL.TO_GEOJSON(GEOMETRY)
                ||'}' 
                FORMAT JSON RETURNING CLOB) 
            ||'}'
            AS GEOJSON
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        

![GeoJSON zurückgeben](images/return-geojson-05.png)

6.  Klicken Sie mit der rechten Maustaste in die Ergebniszelle, und wählen Sie **Kopieren** aus.
    
    ![GeoJSON zurückgeben](images/return-geojson-06.png)
    
7.  Prüfen Sie das Ergebnis durch Rendern. Klicken Sie [hier](http://geojson.io), um geojson.io in einer neuen Browserregisterkarte zu öffnen. Löschen Sie den Inhalt im rechten Fensterbereich unter JSON (alle auswählen > löschen), und fügen Sie ihn aus dem SQL Worksheet in die kopierte Datei GeoJSON ein. Klicken Sie auf eine der Tornado-Linien, um ein Popup mit seinen Eigenschaften anzuzeigen.
    
    ![GeoJSON zurückgeben](images/return-geojson-07.png)
    
8.  Um das Ergebnis etwas interessanter zu gestalten, führen Sie den folgenden Befehl aus, um ein GeoJSON-Dokument mit Geometrien zu erstellen, die 5-Meilen-Puffer um die Tornado-Pfade herum sind. Beachten Sie, dass ein neuer Eigenschaftsschlüssel hinzugefügt wird, um den Pufferabstand anzugeben. Führen Sie die Abfrage aus, und kopieren Sie das Ergebnis wie zuvor.
    
        <copy> 
        SELECT
           '{"type": "FeatureCollection", "features":'
           || JSON_ARRAYAGG( 
               '{"type": "Feature", "properties": {'
               || '"key":"'|| KEY
               ||'","yr":"'|| YR
               ||'","loss":"'|| LOSS
               ||'","buffer":"5 MI'
               ||'"}, "geometry":'|| SDO_UTIL.TO_GEOJSON(
                                      SDO_GEOM.SDO_BUFFER(GEOMETRY, 5, 1, 'unit=MILE'))
               ||'}' 
               FORMAT JSON RETURNING CLOB)   
           ||'}'
           AS GEOJSON
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON zurückgeben](images/return-geojson-08.png)
    
9.  Öffnen Sie eine neue Registerkarte geojson.io, löschen Sie den JSON-Bereich auf der rechten Seite, und fügen Sie das aus dem SQL Worksheet kopierte Ergebnis ein. Beobachten Sie die Puffergeometrien, und klicken Sie auf eine, um ein Popup mit Eigenschaften anzuzeigen, einschließlich des hinzugefügten Pufferschlüssels.
    
    ![GeoJSON zurückgeben](images/return-geojson-09.png)
    

In einem realen Szenario wird die von Ihnen generierte GeoJSON Clients wie der Zuordnung von JavaScript-Librarys und Python-Notizbüchern bereitgestellt, z.B. über JDBC oder APIs, die mit Oracle REST Data Services veröffentlicht werden.

Sie können jetzt **mit der nächsten Übung fortfahren**.

## Weitere Informationen

*   [Räumliches Produktportal](https://oracle.com/goto/spatial)
*   [Räumliche Dokumentation](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Spatial-Blogposts auf Oracle Database Insider](https://blogs.oracle.com/database/category/db-spatial)

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, September 2022