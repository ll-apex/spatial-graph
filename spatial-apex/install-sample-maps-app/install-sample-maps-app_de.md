# Beispielkartenanwendung installieren

## Einführung

Oracle APEX bietet Zugriff auf ein Portfolio von Beispielanwendungen, die bestimmte Funktionsbereiche hervorheben. Dazu gehört die Anwendung Sample Maps, in der die Zuordnungsfunktionen in Oracle APEX dargestellt werden. Als funktionale Beispiele und Ausgangspunkte für die weitere Anpassung werden vielfältige Beispiele gegeben. In dieser Übung installieren und konfigurieren Sie die Anwendung Sample Maps.

Geschätzte Laborzeit: 15 Minuten

### Ziele

*   Installieren Sie die Sample Maps-Anwendung.
*   Unterstützende Daten laden

### Voraussetzungen

*   Oracle APEX 21.1+ ist erforderlich. Die Screenshots in diesem Workshop werden mit APEX 21.2 erstellt. Da wir generell die Verwendung der [neuesten Version von APEX](https://www.oracle.com/tools/downloads/apex-downloads/) empfehlen, erwarten wir gelegentlich kleine Unterschiede in der Benutzeroberfläche.

## Aufgabe 1: Anwendung installieren

1.  Klicken Sie zunächst auf **App Builder**.
    
    ![APEX Application Builder](images/install-sample-maps-00.png)
    
2.  Klicken Sie auf **Start- oder Beispiel-App installieren**.
    
    ![Start- oder Beispielanwendung auswählen](images/install-sample-maps-01.png)
    
    **Hinweis:** Wenn im Workspace Anwendungen vorhanden sind, klicken Sie auf **Erstellen** und dann auf **Starter-App**.
    
3.  Klicken Sie auf **Beispiele**, um eine neue Browserregisterkarte mit einer Liste der verfügbaren Beispielanwendungen zu öffnen.
    
    ![Muster auswählen](images/install-sample-maps-02.png)
    
4.  Scrollen Sie nach unten zu **Beispielzuordnungen**, und klicken Sie auf **App herunterladen**.
    
    ![Alternativer Bildtext](images/install-sample-maps-03.png)
    
    Sie werden aufgefordert, das Anwendungs-Bundle in einem lokalen Ordner zu speichern.
    
    **Hinweis:** Wenn Sie zu github umgeleitet werden, navigieren Sie zum Ordner für Ihre APEX-Version, und laden Sie **sample-maps.zip** herunter.
    
5.  Kehren Sie zur App Builder-Browserregisterkarte zurück. Klicken Sie auf **Importieren**.
    
    ![Import auswählen](images/install-sample-maps-04.png)
    
6.  Ziehen Sie die ZIP-Datei der Anwendung Sample Maps, die Sie zuvor heruntergeladen haben, per Drag-and-Drop, oder navigieren Sie zu ihr. Behalten Sie die Auswahl für den Dateityp bei "Datenbankanwendung", und klicken Sie auf **Weiter**.
    
    ![Anwendungs-ZIP für Beispielzuordnungen auswählen](images/install-sample-maps-05.png)
    
7.  Dateiimport wurde bestätigt. Klicken Sie erneut auf **Weiter**.
    
    ![Klicken Sie auf "Next".](images/install-sample-maps-06.png)
    
8.  Behalten Sie die Standardmenüauswahl bei, und klicken Sie auf **Anwendung installieren**.
    
    ![Klicken Sie auf "Anwendung installieren".](images/install-sample-maps-07.png)
    
    Dadurch gelangen Sie zum Assistenten "Anwendung installieren".
    
9.  Behalten Sie die Standardmenüauswahl bei, und klicken Sie auf **Weiter**.
    
    ![Klicken Sie auf "Next".](images/install-sample-maps-08.png)
    
10.  Klicken Sie auf **Weiter**, um die Systemkompatibilität zu validieren.
    

![Klicken Sie auf "Next".](images/install-sample-maps-09.png)

11.  Wenn die Kompatibilität bestätigt ist, klicken Sie auf **Installieren**, um die Installation unterstützender Datenbankobjekte und der APEX-Anwendung zu initiieren.

![Klicken Sie auf "Installieren".](images/install-sample-maps-10.png)

12.  Klicken Sie nach Abschluss der Installation auf **Anwendung ausführen**.

![Klicken Sie auf "Anwendung ausführen".](images/install-sample-maps-11.png)

13.  Melden Sie sich bei der Anwendung Sample Maps mit Ihrem APEX-Workspace-Benutzernamen und -Kennwort an.

![Anmelden](images/install-sample-maps-12.png)

## Aufgabe 2: Daten laden

1.  Sie befinden sich nun in der Anwendung Sample Maps, die zahlreiche Beispiele für Maps und räumliche Vorgänge in APEX enthält. Beim ersten Start wird eine Warnmeldung zum Laden von Daten angezeigt. Klicken Sie in dieser Nachricht auf den Link **Daten laden**. Sie navigieren zu einer Seite, auf der Sie das Laden der Demodaten abschließen.
    
    ![Klicken Sie auf Daten laden](images/install-sample-maps-13.png)
    
2.  Auf der Seite "Daten laden" wird der Ladestatus der von der Anwendung "Beispielkarten" verwendeten Datensätze für Staaten und Flughäfen und der Rest dieses Workshops angezeigt. Nach der Installation der Anwendung Sample Maps werden diese Datensätze nur teilweise geladen. Um das Laden der Beispieldaten abzuschließen, können Sie entweder direkt aus Dateien laden, die in github gespeichert sind, oder Sie können die Dateien zuerst herunterladen und vom lokalen System laden. Wenn Sie APEX in einem Netzwerk ausführen, für das ein Proxy für den Zugriff auf github erforderlich ist, sollten Sie die letztere Option verwenden.
    
    Wenn für Ihre APEX-Instanz kein Proxy für den Zugriff auf Github erforderlich ist (z.B. APEX.oracle.com oder APEX mit Oracle Autonomous Database), klicken Sie auf die Schaltfläche, um **direkt aus GitHub** zu laden. Klicken Sie dann oben rechts auf **Dataset laden**.
    
    ![Klicken Sie direkt von Github](images/install-sample-maps-14.png)
    
    Wenn für Ihre APEX-Instanz ein Proxy für den Zugriff auf Github erforderlich ist (Beispiel: APEX, der hinter Ihrer Unternehmensfirewall ausgeführt wird), oder wenn andere Probleme beim Laden direkt aus Github auftreten, klicken Sie auf die Schaltfläche **Dateien hochladen**, die alternative Anweisungen enthält.
    
3.  Wenn das Laden der Daten abgeschlossen ist, wird oben rechts eine Benachrichtigung angezeigt, und die Warnmeldung ist nicht mehr vorhanden. Die Anwendung Sample Maps kann jetzt verwendet werden.
    
    ![Bestätigung zum Laden der Daten](images/install-sample-maps-15.png)
    

## Aufgabe 3: Beispielkartenanwendung untersuchen

1.  Wenn Sie auf eine der Kacheln klicken, wird die zugehörige Seite in der Anwendung aufgerufen. Klicken Sie beispielsweise auf **Zuordnen und Bericht**.
    
    ![Zur Seite "Zuordnung und Bericht" navigieren](images/install-sample-maps-16.png)
    
2.  Klicken Sie auf dieser Seite auf ein Element im Bericht in der rechten Mitte des Elements in der Karte, und öffnen Sie ein Infofenster. Wenn Sie auf das Symbol in der oberen linken Ecke klicken, wird ein Navigationsbereich geöffnet, um auf andere Seiten in der Anwendung zuzugreifen.
    
    ![Interagieren Sie mit der Karte](images/install-sample-maps-17.png)
    
3.  Klicken Sie auf Elemente im Navigationsbereich, um auf andere Seiten in der Anwendung zuzugreifen.
    
    ![Navigationsbereich zeigt andere Seiten](images/install-sample-maps-18.png)
    
4.  Um den Navigationsbereich zu schließen, klicken Sie auf das Symbol oben links. Sie können auch zur Homepage der Anwendung navigieren, indem Sie oben links auf **Beispielzuordnungen** klicken.
    
    ![Navigationsbereich schließen](images/install-sample-maps-19.png)
    

## Aufgabe 4: Demodaten untersuchen

1.  Kehren Sie zu APEX zurück, klicken Sie auf **SQL Workshop** und dann auf **Object Browser**.
    
    ![SQL Workshop - Object Browser](images/install-sample-maps-20.png)
    
2.  Beachten Sie die Tabellen, die durch den zuvor ausgeführten Dataload-Schritt erstellt wurden. Klicken Sie auf **EBA\_SAMPLE\_MAP\_AIRPORTS**. Beachten Sie, dass die Spalten eine Spalte namens GEOMETRY mit dem Typ SDO\_GEOMETRY (nativer räumlicher Datentyp von Oracle) enthalten.
    
    ![Tabelle mit nativer Geometriespalte](images/install-sample-maps-21.png)
    
3.  Klicken Sie auf die Registerkarte **Daten**, um den Tabelleninhalt anzuzeigen.
    
    ![Tabelleninhalt](images/install-sample-maps-22.png)
    
    Scrollen Sie dann nach rechts, um die Geometriespalte anzuzeigen. Da Flughäfen als Punkte gespeichert werden, zeigt APEX eine Zeichenfolgendarstellung des Punktgeometriewerts an. Punkte basieren immer auf einer einzigen Koordinate, sodass APEX den Wert auf diese Weise anzeigen kann.
    
    ![Punktgeometrien](images/install-sample-maps-23.png)
    
4.  Klicken Sie auf **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES**. Beachten Sie auch hier, dass die Spalten eine Spalte namens GEOMETRY mit dem Typ SDO\_GEOMETRY (nativer räumlicher Datentyp von Oracle) enthalten.
    
    ![Tabelle mit nativer Geometriespalte](images/install-sample-maps-24.png)
    
5.  Klicken Sie auf die Registerkarte **Daten**, um den Tabelleninhalt anzuzeigen. Da diese Tabelle Zustände speichert, sind die Geometrien Polygone. APEX zeigt keine Zeichenfolgendarstellung dieser Werte an, da sie extrem lange Koordinatensets enthalten können.
    
    ![Polygongeometrien](images/install-sample-maps-25.png)
    
6.  Beachten Sie die Tabellen mit Namen wie **MDRT\_....$**. Diese werden von der Datenbank automatisch im Hintergrund erstellt und verwaltet, um Spatial Indexes für andere Tabellen zu unterstützen. Sie können diese Tabellen niemals manuell erstellen, aktualisieren oder löschen. Sie dienen ausschließlich der Unterstützung von räumlichen Analysevorgängen und können ignoriert werden.
    
    ![Räumliche Indexartefakte](images/install-sample-maps-26.png)
    
7.  Schließlich können Sie mit diesen Daten eine allgemeine räumliche Abfrage ausführen. Klicken Sie auf **SQL Workshop** und dann auf **SQL Commands**.
    
    ![SQL Workshop - SQL-Befehle](images/install-sample-maps-27.png)
    
8.  Die folgende Abfrage gibt die Anzahl der Flughäfen mit einer Landdeckung von über 1000 Hektar innerhalb von 100 km von Texas zurück. Beachten Sie die Verwendung des nativen Spatial-Operators **sdo\_within\_distance**. Kopieren Sie die Abfrage, und fügen Sie sie in das Fenster "SQL Commands" ein. Klicken Sie dann oben rechts auf **Run**.
    
        <copy>
        select count(a.id) as number_of_airports
        from EBA_SAMPLE_MAP_AIRPORTS a,
              EBA_SAMPLE_MAP_SIMPLE_STATES b
        where b.state_code= 'TX'
           and land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance=100 unit=KM') = 'TRUE'
        </copy>
        
    
    ![Räumliche Abfrage](images/install-sample-maps-28.png)
    
9.  Aktualisieren Sie im Operator sdo\_within\_distance die Entfernung auf 300 km, und führen Sie sie erneut aus. Beachten Sie die Ergebnisänderungen basierend auf dem größeren Suchbereich.
    
    ![Räumliche Abfrage](images/install-sample-maps-29.png)
    

In einer späteren Übung konfigurieren Sie eine Karte, in der die Ergebnisse dieser Abfrage angezeigt werden. Dabei werden Status und Entfernung von den Menüs auf der Seite gesteuert.

Sie haben jetzt die Sample Maps-Anwendung und die Daten installiert und untersucht. Als Nächstes beginnen Sie mit der Erstellung Ihrer eigenen Anwendung und Karten.

Damit endet das Labor. Sie können jetzt mit der nächsten Übung fortfahren.

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Mitwirkende** - Carsten Czarski, APEX Development, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, Database Product Management, März 2023