# Datenexplorer

## Einführung

Sie untersuchen jetzt die in der vorherigen Übung vorbereiteten Standort- und Transaktionsdaten. Durch die Verwaltung der Daten in Autonomous Database können Sie Backend-Verarbeitungs- und -Analysevorgänge ausführen und dann entsprechende Datenteilmengen für spezielle Analysen in Python integrieren.

Geschätzte Laborzeit: 10 Minuten

### Ziele

*   Spatiotemporale Daten und Abfrageergebnisse aus Autonomous Database in Python integrieren
*   Daten in Python visualisieren und untersuchen

### Voraussetzungen

*   Abschluss von Übung 5: Daten vorbereiten

## Aufgabe 1: Spatial Data Handling in Python

Die häufigste Python-Bibliothek für die Datenverarbeitung ist Pandas, das DataFrame als Datenstruktur bereitstellt, die einer Tabelle mit Spalten und Zeilen ähnelt. Die GeoPandas-Bibliothek erweitert Pandas für die Verarbeitung räumlicher Daten, wobei DataFrame auf GeoDataFrame einschließlich einer "Geometrie"-Spalte erweitert wird. Die Shapely-Bibliothek stellt den räumlichen Typ bereit, der zum Auffüllen der Geometriespalte verwendet wird. Folium ist eine beliebte Kartenvisualisierungsbibliothek und wird von GeoPandas verwendet.

1.  Importieren Sie Bibliotheken für die Verarbeitung räumlicher Daten und die Kartenvisualisierung.
    
        <copy>
        import geopandas as gpd
        import shapely
        import folium
        </copy>
        
    
    ![Datenexplorer](images/explore-data-01.png)
    
2.  Führen Sie als grundlegendes Beispiel für räumliche Daten in Python den folgenden Befehl aus, um manuell eine GeoDataFrame mit Punktstandorten für mehrere Städte zu erstellen. Die Geometriewerte haben das Format Well-Known Text ("WKT"), da dies das Format ist, das in einem GeoDataFrame verwendet wird.
    
        <copy>
        gdf = gpd.GeoDataFrame(
          {
            "city": ["Buenos Aires", "Brasilia", "Santiago", "Bogota", "Caracas"],
            "country": ["Argentina", "Brazil", "Chile", "Colombia", "Venezuela"],
            "geometry": ["POINT(-58.66 -34.58)",
                         "POINT(-47.91 -15.78)",
                         "POINT(-70.66 -33.45)",
                         "POINT(-74.08 4.60)",
                         "POINT(-66.86 10.48)",
                ],})
        gdf["geometry"] = gpd.GeoSeries.from_wkt(gdf["geometry"])
        gdf.set_geometry("geometry")
        gdf.crs="EPSG:4326"
        gdf
        </copy>
        
    
    ![Datenexplorer](images/explore-data-02.png)
    
3.  Um die Daten zu visualisieren, führen Sie den folgenden Befehl aus, in dem Sie sowohl die Hintergrundkarte als auch die Markergröße angeben. Bewegen Sie die Maus über einen Kartenmarker, um seine Attribute anzuzeigen.
    
        <copy>
        gdf.explore(tiles="CartoDB positron", marker_kwds={"radius":8})
        </copy>
        
    
    ![Datenexplorer](images/explore-data-03.png)
    
4.  Oracle Spatial umfasst Funktionen und Methoden zur Konvertierung vom nativen Spatial-Typ in gängige Formate, einschließlich der Konvertierung in das WKT-Format, das in einem GeoDataFrame verwendet wird. Das Erstellen einer GeoDataFrame aus Oracle Spatial-Ergebnissen ist also einfach. Die Konvertierungssyntax von Objektmethoden ist kompakter als die entsprechenden SQL-Funktionen. Beispiel: Die Methode **(geometry).get\_wkt()** im Vergleich zur Funktion **sdo\_util.to\_wktgeometry(geometry)**. Führen Sie den folgenden Befehl aus, um ein einfaches Beispiel für Formatkonvertierungen von hartcodierten Formaten SDO\_GEOMETRY in WKT und GeoJSON mit Objektmethoden anzuzeigen.
    

    ```
    <copy>
    cursor = connection.cursor()
    cursor.execute("""
      WITH x AS (
        SELECT sdo_geometry(2001,4326,sdo_point_type(-100.12, 22.34,null),null,null) 
               as geometry
        FROM dual)
      SELECT geometry, 
             (geometry).get_wkt(), 
             (geometry).get_geojson()
      FROM x
      """)
    for row in cursor.fetchone():
       print(row)
    </copy>
    ```
    ![Explore data](images/explore-data-04.png) 
    

5.  In der vorherigen Übung haben Sie die Tabelle LOCATIONS mit einem funktionsbasierten Spatial Index konfiguriert. Die Funktion ist lonlat\_to\_proj\_geom( ) und konvertiert Längen- und Breitengrad in ein SDO\_GEOMETRY im World Mercator-Koordinatensystem zur Kompatibilität mit Bibliotheken, die in einer späteren Übung verwendet werden. Führen Sie den folgenden Befehl aus, um Geometrien mit dieser Funktion als WKT-Format abzurufen.

    ```
    <copy>
    cursor = connection.cursor()
    cursor.execute("""
      SELECT lon, lat, (lonlat_to_proj_geom(lon,lat)).get_wkt()
      FROM locations
      """)
    for row in cursor.fetchmany(10):
       print(row)
    </copy>
    ```
    ![Explore data](images/explore-data-05.png) 
    

6.  Führen Sie den folgenden Befehl aus, um die Tabelle LOCATIONS abzurufen und eine GeoDataFrame zu erstellen.
    
        <copy>
        cursor.execute("""
         SELECT location_id, owner, (lonlat_to_proj_geom(lon,lat)).get_wkt()
         FROM locations
         """)
        gdf = gpd.GeoDataFrame(cursor.fetchall(), columns = ['location_id', 'owner', 'geometry'])
        gdf['geometry'] = shapely.from_wkt(gdf['geometry'])
        gdf.crs="EPSG:3857"
        gdf.head()
        </copy>
        
    
    ![Datenexplorer](images/explore-data-06.png)
    
7.  Führen Sie den folgenden Befehl aus, um GeoDataFrame zu visualisieren.
    
        <copy>
        gdf.explore(tiles="CartoDB positron")
        </copy>
        
    
    ![Datenexplorer](images/explore-data-07.png)
    

## Aufgabe 2: Transaktionsdaten untersuchen

1.  Als Nächstes erstellen Sie eine GeoDataFrame aus einer Abfrage, die TRANSACTIONS mit LOCATIONS verknüpft. Führen Sie den folgenden Befehl aus, um die GeoDataFrame zu erstellen.
    
        <copy>
        cursor = connection.cursor()
        cursor.execute("""
         SELECT a.cust_id, a.trans_id, a.trans_epoch_date, 
          (lonlat_to_proj_geom(b.lon,b.lat)).get_wkt() 
         FROM transactions a, locations b
         WHERE a.location_id=b.location_id
         """)
        gdf = gpd.GeoDataFrame(cursor.fetchall(), columns = ['cust_id', 'trans_id', 'trans_epoch_date', 'geometry'])
        gdf['geometry'] = shapely.from_wkt(gdf['geometry'])
        gdf.crs="EPSG:3857"
        gdf.head()
        </copy>
        
    
    ![Datenexplorer](images/explore-data-08.png)
    
2.  Führen Sie den folgenden Befehl aus, um GeoDataFrame zu visualisieren. Bewegen Sie den Mauszeiger über einen Artikel, um Transaktionsattribute anzuzeigen.
    
        <copy>
        gdf.explore(tiles="CartoDB positron") 
        </copy>
        
    
    ![Datenexplorer](images/explore-data-09.png)
    

Sie können jetzt **mit der nächsten Übung fortfahren**.

## Weitere Informationen

*   Einzelheiten zu GeoPandas finden Sie unter [https://geopandas.org](https://geopandas.org)

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Mitwirkende** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Zuletzt aktualisiert am/um** - David Lapp, August 2023