# Map mit Assistent erstellen

## Einführung

Oracle APEX bietet einen Assistenten zum Erstellen einer Vielzahl nützlicher Seitentypen. In dieser Übung erstellen Sie mit dem Assistenten eine neue Anwendung und eine Seite mit einer Karte. Anschließend prüfen Sie die resultierende Seite, um die Map Region zu verstehen.

Geschätzte Laborzeit: 10 Minuten

### Ziele

*   APEX-Mapregion - Grundlagen

### Voraussetzungen

*   Abschluss von Übung 1: Anwendung "Beispielzuordnungen installieren"

## Aufgabe 1: Neue App mit einer Kartenseite mit dem Assistenten erstellen

Der Assistent bietet eine schnelle und einfache Möglichkeit, eine neue Anwendung und Ihre erste Karte zu erstellen.

1.  Navigieren Sie zum **App Builder**, und klicken Sie auf **Erstellen**. ![Assistent "Anwendung erstellen" in App Builder](images/create-map-01.png)
    
2.  Wählen Sie **Neue Anwendung** aus. ![Anwendung erstellen - Neue Anwendung](images/create-map-02.png)
    
3.  Geben Sie einen Namen für die Anwendung ein, und klicken Sie auf **Seite hinzufügen**. ![Antrag erstellen - Formular](images/create-map-03.png)
    
4.  Wählen Sie **Map** als Seitentyp. ![Anwendung erstellen - Seite hinzufügen](images/create-map-04.png)
    
    **Hinweis**: Dies ist derselbe Assistent wie die Verwendung von **Seite erstellen** in einer vorhandenen Anwendung.
    
5.  Geben Sie **Flughafenkarte** als Seitenname ein. (Mit diesem Assistenten wird der Seitenname auch als Name der auf der Seite erstellten Kartenregion verwendet.) Klicken Sie auf das Symbol rechts neben der Tabelleneingabe, um die Tabelle **EBA\_SAMPLE\_MAP\_AIRPORTS** auszuwählen. Wählen Sie für die Geometriespalte **GEOMETRY** aus, und wählen Sie schließlich eine Spalte aus, um beim Mouseover auf ein Element in der Karte eine QuickInfo zu verwenden. ![Anwendung erstellen - Seite "Karte erstellen"](images/create-map-05.png)
    
6.  Beachten Sie, dass die neue Seite jetzt unter **Seiten** aufgeführt wird. Klicken Sie auf **Anwendung erstellen**. ![Anwendung erstellen - Erstellung der Anwendung abschließen](images/create-map-06.png)
    
7.  Sie werden zu der Seite weitergeleitet, auf der Sie die neue Anwendung verwalten. Klicken Sie auf **Anwendung ausführen**. ![Anwendung ausführen](images/create-map-07.png)
    
8.  Melden Sie sich bei Ihrer Anwendung mit Ihrem APEX-Anmeldenamen und -Kennwort an. ![Bei Ihrer Anwendung anmelden](images/create-map-08.png)
    
9.  Das für unsere Anwendung ausgewählte Standardlayout bietet eine Homepage mit Links zu anderen Seiten. Navigieren Sie von der Homepage zur gerade erstellten Seite. ![Anwendungshomepage](images/create-map-09.png)
    
10.  Beobachten Sie die Seite mit einer interaktiven Karte, die Flughafenstandorte mit den von Ihnen konfigurierten QuickInfos anzeigt. ![Karte anzeigen](images/create-map-10.png)
    

## Aufgabe 2: Seite "Map" prüfen

Sie prüfen nun die vom Assistenten erstellte Map Region.

1.  Klicken Sie in der Entwicklersymbolleiste unten auf der Seite auf die Schaltfläche **Seite 2**, um die Seite zu bearbeiten. ![Seite bearbeiten](images/create-map-11.png)
    
2.  Klicken Sie in der Seitenstruktur auf der linken Seite unter **Hauptteil** auf **Flughafenkarte**. Dies ist der Titel des Map-Bereichs, der mit dem Assistenten "Seite erstellen" erstellt wurde. Sie ist standardmäßig mit dem Seitentitel identisch und kann beliebig geändert werden. Beachten Sie im Bereich mit den Regionsdetails auf der rechten Seite, dass diese Region den Typ **Map** aufweist. ![Seiteneigenschaften anzeigen](images/create-map-12.png)
    
3.  Zu den Kartenregionen gehören Ebenen, bei denen es sich um Punkte, Linien und Polygone (von Oracle Spatial, GeoJSON oder Koordinaten) handelt, die auf einer Hintergrundkarte angezeigt werden. Wenn Sie den Assistenten "Seite erstellen" durchlaufen, haben Sie eine Karte mit der Spalte GEOMETRY in Tabelle EBA\_SAMPLE\_MAP\_AIRPORTS (d.h. Oracle Spatial-Daten) ausgewählt. Der Assistent hat also eine Ebene erstellt, die diese Flughafenstandorte enthält. Standardmäßig hat die Ebene denselben Namen wie die Seite, d.h. **Flughafenkarte**. Dies kann beliebig geändert werden.
    
    Um diese Ebene zu prüfen, klicken Sie in der Seitenstruktur im linken Bereich unter "Ebenen" auf **Flughafenkarte**. Konfigurationsdetails werden im Bereich **Ebene** auf der rechten Seite angezeigt. Informationen zu Konfigurationselementen erhalten Sie, wenn Sie im mittleren Fensterbereich auf die Registerkarte **Hilfe** klicken. Wenn Sie dann auf Konfigurationselemente klicken, werden Hilfeinformationen für dieses Element angezeigt. Beispiel: Klicken Sie in das Menü **Layertyp**, um Hilfe zu den Optionen anzuzeigen. ![Eigenschaften von Kartenlayer prüfen](images/create-map-13.png)
    
4.  Scrollen Sie im Bereich "Layer" nach unten, um die anderen Konfigurationsoptionen anzuzeigen, die vom Assistenten festgelegt wurden, einschließlich der Spaltenzuordnung, in der der Geometriedatentyp festgelegt ist. Hier verwenden Sie den nativen räumlichen Datentyp SDO\_GEOMETRY von Oracle, und der Spaltenname lautet GEOMETRY. ![Eigenschaften von Kartenlayer prüfen](images/create-map-14.png)
    

Herzlichen Glückwunsch zum Erstellen Ihrer ersten Karten. Es gibt eine Menge Fähigkeiten jenseits der Grundlagen, die Sie gerade erforscht haben. Fühlen Sie sich frei, mit Anpassungen an Parametern zu experimentieren und dann zu speichern und auszuführen, um Ergebnisse anzuzeigen. In der nächsten Übung konfigurieren Sie eine ganz neue Kartenregion.

Damit endet das Labor. Sie können jetzt mit der nächsten Übung fortfahren.

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, Database Product Management, März 2023