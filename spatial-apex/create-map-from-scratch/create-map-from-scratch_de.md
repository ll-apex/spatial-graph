# Map neu erstellen

## Einführung

In dieser Übung erstellen Sie eine neue Seite in der Anwendung und konfigurieren dann eine ganz neue Map-Region.

Geschätzte Laborzeit: 15 Minuten

### Ziele

*   Konfiguration der APEX-Zuordnungsregion verstehen

### Voraussetzungen

*   Übung 2: Karte mit Assistent erstellen

## Aufgabe 1: Neue Seite erstellen

1.  Klicken Sie in den Navigationspfaden oben links auf den Link für Ihr Anwendungs-Home. Klicken Sie dann auf die Registerkarte **Layout**. ![Seitenlayout](images/create-map-15a.png)
    
2.  Klicken Sie auf **Seite erstellen**. ![Assistent Seite erstellen](images/create-map-15b.png)
    
3.  Sie können hier "Map" auswählen, um denselben Assistenten wie im Assistenten "App erstellen" zu verwenden. Dieser Schritt besteht jedoch darin, eine Karte von Grund auf neu zu erstellen, beispielsweise wenn Sie eine vorhandene Seite haben. Wählen Sie **Leere Seite** aus, und klicken Sie auf **Weiter**. ![Leere Seite auswählen](images/create-map-16.png)
    
4.  Geben Sie als Namen **Flughafen- und Statuskarte** ein, und klicken Sie auf **Weiter**. ![Seitennamen eingeben](images/create-map-16a.png)
    
5.  Wählen Sie die Option, um einen neuen Navigationsmenüeintrag zu erstellen, und geben Sie **Flughäfen und Staatenkarte** ein, d.h. denselben Seitennamen. Klicken Sie dann auf **Weiter**. ![Navigationsmenüeintrag erstellen](images/create-map-17.png)
    
6.  Prüfen Sie die Übersicht, und klicken Sie auf **Beenden**. ![Übersicht prüfen](images/create-map-18.png)
    

## Aufgabe 2: Seite eine Karte hinzufügen

1.  Ziehen Sie **Zuordnen** aus der Palette "Regionen" unten, und legen Sie sie unter dem Abschnitt "Text" des Seitenlayouts ab. Beachten Sie, dass der Kartenbereich im Seitenbaum unter Body mit dem Standardnamen "Neu" angezeigt wird. Klicken Sie im Seitenbaum auf **Neu**, und beobachten Sie die Eigenschaften rechts. Beachten Sie, dass der Regionstyp "Map" lautet. ![Kartenbereich hinzufügen](images/create-map-19.png)
    
2.  Aktualisieren Sie im Bereich auf der rechten Seite den Regionstitel von "Neu" in einen Namen Ihrer Wahl. Beispiel: **Meine Kartenregion**. Beachten Sie, dass der Titel im Seitenbaum auf der linken Seite aktualisiert wird. ![Regionstitel eingeben](images/create-map-20.png)
    
3.  Beachten Sie, dass der Kartenbereich ein untergeordnetes Element mit der Bezeichnung "Layer" und der Default-Ebene "New" enthält. Ebenen sind die datengesteuerten Inhalte, die auf der Karte wiedergegeben werden sollen. Klicken Sie im Seitenbaum auf den Layer **Neu**, um dessen Eigenschaften im rechten Fensterbereich anzuzeigen. ![Ebeneneigenschaften anzeigen](images/create-map-21.png)
    
4.  Aktualisieren Sie den Layer-Namen in **Flughäfen** und den Typ in **Punkte**. Beachten Sie die Aktualisierung des Ebenennamens im Seitenbaum auf der linken Seite. ![Layer-Eigenschaften aktualisieren](images/create-map-23.png)
    
5.  Scrollen Sie im Eigenschaftsbereich "Layer" auf der rechten Seite nach unten. Aktualisieren Sie die **Quelle**, um die Tabelle **EBA\_SAMPLE\_MAP\_AIRPORTS** zu verwenden. Um die in der Ebene gerenderten Flughäfen zu begrenzen, fügen Sie die Where-Klausel **LAND\_AREA\_COVERED > 2500** hinzu. Aktivieren Sie die Option "Spatial Index verwenden" mit dem Switch. ![Layer-Eigenschaften aktualisieren](images/create-map-24.png)
    
6.  Scrollen Sie im Bereich "Layer-Eigenschaften" rechts nach unten zum Abschnitt **Spaltenzuordnung**. Hier konfigurieren Sie die räumliche Spalte für die Wiedergabe. Wählen Sie den Geometriedatentyp **SDO\_GEOMETRY** und die Geometriespalte **GEOMETRY** aus. ![Layer-Eigenschaften aktualisieren](images/create-map-25.png)
    
7.  Scrollen Sie im Bereich "Layer-Eigenschaften" rechts nach unten zum Abschnitt **Infofenster**. Hier können Sie den Inhalt eines Informationsfensters konfigurieren, das beim Klicken auf ein Element in der Karte angezeigt wird. Aktivieren Sie die **Erweiterte Formatierung**, indem Sie auf die Schaltfläche "Umschalten" klicken, und fügen Sie Folgendes in den Textbereich **HTML-Ausdruck** ein:
    
        <copy>
        <strong>&AIRPORT_NAME.</strong><br>
        &CITY., &STATE_NAME.<br>
        Code: &IATA_CODE.
        </copy>
        
    
    ![Layer-Eigenschaften aktualisieren](images/create-map-25a.png)
    

## Aufgabe 3: Layer zur Karte hinzufügen

1.  Klicken Sie im Seitenbaum auf der linken Seite unter dem Kartenbereich mit der rechten Maustaste auf **Layer**, und wählen Sie **Layer erstellen** aus. ![Ebene hinzufügen](images/create-map-26.png)
    
2.  Klicken Sie im Seitenbaum unter Ihrer Kartenregion auf die neu erstellte Ebene. Aktualisieren Sie dann im Bereich "Layer-Details" auf der rechten Seite den Namen in **Status**, den Layer-Typ in **Polygone** und die Quelle in **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES**. ![Layer-Eigenschaften aktualisieren](images/create-map-27.png)
    
3.  Ebenen werden in der Reihenfolge wiedergegeben, in der sie im Seitenbaum unter Ebenen angezeigt werden. Um die Darstellung von Flughäfen auf den obersten Status zu ermöglichen, ziehen Sie die Ebene **Status** über die Ebene "Flughäfen" unter "Ebenen" in der Seitenstruktur. Scrollen Sie im Bereich "Layer-Details" rechts zum Abschnitt "Spaltenzuordnung". Wählen Sie den Geometriedatentyp **SDO\_GEOMETRY** und die Geometriespalte **GEOMETRY** aus. Wählen Sie unter Aussehen eine Füll- und Strichfarbe (Gliederung) Ihrer Wahl aus. Stellen Sie die Füllundurchsichtigkeit auf einen Wert Ihrer Wahl ein, und beachten Sie, dass ein Wert von 1 vollständig undurchsichtig bedeutet, damit die Hintergrundkarte nicht sichtbar ist. ![Layer-Reihenfolge aktualisieren](images/create-map-28.png)
    
4.  Klicken Sie oben rechts auf **Speichern** und dann auf die grüne Schaltfläche **Ausführen**. ![Seite speichern und ausführen](images/create-map-29.png)
    
5.  Beobachten Sie Ihr Karten-Rendering mit Staaten und Flughäfen Ebenen. Klicken und ziehen Sie die Karte in den Schwenkbereich, und verwenden Sie das Navigationssteuerelement oben rechts, um zu vergrößern und zu verkleinern. Klicken Sie auf einen Flughafen, um das von Ihnen konfigurierte Informationsfenster anzuzeigen. Bewegen Sie den Mauszeiger über einen Status, um die konfigurierte QuickInfo anzuzeigen. Schalten Sie Ebenen mit den Kontrollkästchen unter der Karte aus und ein. ![Interagieren Sie mit der Karte](images/create-map-30.png)
    

Herzlichen Glückwunsch zum Erstellen Ihrer ersten Karte. In der nächsten Übung integrieren Sie räumliche Analysen in diese Karte.

Damit endet das Labor. Sie können jetzt mit der nächsten Übung fortfahren.

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, Database Product Management, März 2023