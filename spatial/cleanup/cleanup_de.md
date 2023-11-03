# ADB auf Pre-Workshop-Status zurücksetzen

## Einführung

In dieser Übung werden alle in den vorherigen Übungen erstellten Elemente entfernt, sodass Sie bei Bedarf von vorne beginnen können.

Geschätzte Laborzeit: 2 Minuten

### Info

In dieser Übung werden alle zuvor erstellten Artefakte gelöscht.

### Ziele

*   Setzen Sie die ADB auf den Status vor dem Workshop zurück.

### Voraussetzungen

*   Abschluss von Übung 3; Räumliche Daten vorbereiten

## Aufgabe 1: Alle in diesem Workshop erstellten Elemente entfernen

1.  Um Tabellen und Indizes zu entfernen, die in diesem Workshop erstellt wurden, führen Sie den folgenden Befehl mit der Schaltfläche "Skript ausführen" in SQL Worksheet aus.
    
    ![Alternativer Bildtext](images/run-script.png)
    
        <copy> 
        DROP TABLE WAREHOUSES;
        DROP TABLE STORES;
        DROP TABLE REGIONS;
        DROP TABLE TORNADO_PATHS;
        </copy>
        
2.  Um in diesen Workshop eingefügte räumliche Metadaten zu löschen, führen Sie den folgenden Befehl mit der Schaltfläche "Skript ausführen" in SQL Worksheet aus.
    
        <copy> 
        DELETE FROM USER_SDO_GEOM_METADATA
        WHERE TABLE_NAME IN (
            'WAREHOUSES', 
            'STORES', 
            'REGIONS', 
            'TORNADO_PATHS');
        COMMIT;
        </copy>
        
3.  Um die in diesem Workshop erstellte Funktion zu löschen, führen Sie den folgenden Befehl aus.
    
        <copy> 
        DROP FUNCTION GET_GEOMETRY;
        </copy>
        

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, September 2022