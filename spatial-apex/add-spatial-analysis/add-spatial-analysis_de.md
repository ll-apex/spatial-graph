# Räumliche Analyse integrieren

## Einführung

In dieser Übung erweitern Sie Ihre Karte aus der vorherigen Übung, indem Sie eine räumliche Analyse integrieren. Sie konfigurieren eine Suche nach Flughäfen, die sich in einer benutzerdefinierten Entfernung eines ausgewählten Bundesstaates befinden.

Geschätzte Laborzeit: 30 Minuten

### Ziele

*   Grundlegende räumliche Analysevorgänge verstehen
*   Integration räumlicher Analysen in die APEX-Kartenregion verstehen

### Voraussetzungen

*   Übung 3: Karte von Grund auf neu erstellen

## Aufgabe 1: Region für Filter hinzufügen

1.  Klicken Sie auf die **Seite 3: Karte der Flughäfen und Staaten** oben im Baum auf der linken Seite. Ändern Sie dann im Bereich "Seiteneigenschaften" auf der rechten Seite unter "Darstellung" die Seitenvorlage in **Linke Seitenspalte**.
    
    ![Seitenvorlage aktualisieren](images/add-spatial-analysis-01a.png)
    
    Im Layout sollte dann **LEFTE SPALTE** angezeigt werden.
    
    ![Seitenvorlage aktualisieren](images/add-spatial-analysis-01b.png)
    
2.  Ziehen Sie einen Bereich "Statischer Inhalt" in die linke Spalte.
    
    ![Bereich für statischen Inhalt hinzufügen](images/add-spatial-analysis-01c.png)
    
3.  Benennen Sie in **Bereich "Meine Filter"** oder einen Namen Ihrer Wahl um.
    
    ![Region umbenennen](images/add-spatial-analysis-02.png)
    

## Aufgabe 2: Element zur Statusauswahl hinzufügen

1.  Ziehen Sie ein Auswahllistenelement in den Filterbereich, und aktualisieren Sie den Namen in **P3\_STATE**.
    
    ![Auswahllistenelement hinzufügen](images/add-spatial-analysis-03.png)
    
2.  Blättern Sie in den Eigenschaften des Seitenelements auf der rechten Seite mit der Bildlaufleiste nach unten zum Abschnitt für die Werteliste. Aktivieren Sie **Wert erforderlich** mit dem Switch, setzen Sie den Typ auf **SQL-Abfrage**, und geben Sie die folgende Abfrage ein:
    
        <copy>
          select name, state_code
            from EBA_SAMPLE_MAP_SIMPLE_STATES
        order by name
        </copy>
        
    
    ![SELECT-Abfrage](images/add-spatial-analysis-04.png)
    
3.  Blättern Sie in den Eigenschaften des Seitenelements rechts nach unten zum Abschnitt "Standard". Setzen Sie den Typ auf **Statisch** und den Wert auf **"Texas"** oder einen anderen Status Ihrer Wahl (in einfachen Anführungszeichen).
    
    ![Auswahlliste konfigurieren](images/add-spatial-analysis-05.png)
    

## Aufgabe 3: Artikel für Entfernungseingabe hinzufügen

1.  Ziehen Sie das Zahlenfeld in den Filterbereich. Aktualisieren Sie den Namen in **P3\_DISTANCE** und das Label in **Proximity (km)**.
    
    ![Zahlenfeldelement hinzufügen](images/add-spatial-analysis-06.png)
    
2.  Blättern Sie in den Eigenschaften des Seitenelements rechts nach unten zum Abschnitt "Validierung", und aktivieren Sie **Wert erforderlich**.
    
    ![Validierung auf "Wert erforderlich" setzen](images/add-spatial-analysis-07.png)
    
3.  Blättern Sie nach unten zum Abschnitt "Standard". Setzen Sie den Typ auf **Static**, und Wert auf **100**.
    
    ![Standardwert festlegen](images/add-spatial-analysis-08.png)
    
    Sie haben jetzt Eingaben zum Filtern von Flughäfen nach der Nähe eines Staates. Als Nächstes wenden Sie die Filter mit dynamischen Aktionen an.
    

## Aufgabe 4: Filter mit dynamischen Aktionen anwenden

Als Nächstes erstellen Sie die Aktionen, die aufgerufen werden, wenn Status- und/oder Entfernungswerte vom Benutzer geändert werden.

1.  Klicken Sie mit der rechten Maustaste auf das Element P3\_STATE oder P3\_DISTANCE, und wählen Sie **Dynamische Aktion erstellen** aus (die von uns erstellte Aktion wird auf beide Elemente angewendet).
    
    ![Dynamische Aktion erstellen](images/add-spatial-analysis-09.png)
    
2.  Setzen Sie in den Eigenschaften der dynamischen Aktion auf der rechten Seite den Namen auf **Validieren und aktualisieren**. Setzen Sie im Abschnitt "Wenn" das Ereignis auf **Ändern**, den Auswahltyp auf **Elemente** und Elemente auf die durch Komma getrennte Liste **P3\_DISTANCE,P3\_STATE**. Beachten Sie, dass Sie mit der Schaltfläche rechts neben dem Textfeld Elemente aus einer Liste auswählen können. Um zu verhindern, dass negative Werte für die Entfernung übermittelt werden, setzen Sie im Abschnitt "Clientseite - Bedingung" den Typ auf **Artikel >= Wert**, das Element auf **P3\_DISTANCE** und den Wert auf **0**.
    
    ![Dynamische Aktion konfigurieren](images/add-spatial-analysis-10.png)
    
3.  Dynamische Aktionen werden mit TRUE-Aktionen und FALSE-Aktionen konfiguriert, die basierend auf konfigurierten Bedingungen aufgerufen werden. In diesem Fall bestimmt die clientseitige Bedingung (P3\_DISTANCE >= 0), ob die TRUE-Aktion (Bedingung ist erfüllt) oder die FALSE-Aktion (Bedingung ist nicht erfüllt) aufgerufen werden soll. Dadurch können wir negative Entfernungseingaben einfangen.
    
    Wenn die clientseitige Bedingung TRUE ist, muss die Aktion die Eingabewerte weiterleiten und die Seite aktualisieren. Klicken Sie auf die Aktion unter Wahr. Setzen Sie in den Aktionseigenschaften auf der rechten Seite unter "Identifikation" die Aktion auf **Aktualisieren**. Setzen Sie unter "Betroffene Elemente" den Auswahltyp auf **Region** und "Region" auf **Meine Kartenregion** (oder den Namen, den Sie bei einer anderen Verwendung verwendet haben). Beobachten Sie im Seitenbaum auf der linken Seite, dass sich die Aktion "True" in "Aktualisieren" ändert.
    
    ![Dynamische Aktion konfigurieren](images/add-spatial-analysis-11.png)
    
4.  Als Nächstes konfigurieren Sie die Aktion so, dass sie aufgerufen wird, wenn die clientseitige Bedingung nicht erfüllt ist, was bedeutet, dass ein negativer Entfernungswert eingegeben wurde. Klicken Sie unter "Dynamische Aktionen" für eines der Elemente mit der rechten Maustaste auf "Falsch", und wählen Sie **Falschaktion erstellen** aus.
    
    ![Dynamische Aktion konfigurieren](images/add-spatial-analysis-12.png)
    
5.  Die FALSE-Aktion, die aufgerufen wird, wenn die Entfernung negativ ist, wird dem Benutzer als Popup-Meldung angezeigt. Klicken Sie auf die Aktion "Falsch". Setzen Sie in den Aktionseigenschaften auf der rechten Seite unter "Identifikation" die Aktion auf **Alert**. Legen Sie unter "Einstellungen" den Titel auf **Ungültiger Abstand** fest (dies ist das Alertbanner), und "Nachricht an **Abstand muss >= 0** sein (dies ist der Alertbody). Beachten Sie in der Seitenstruktur auf der linken Seite, dass die Aktion "Falsch" in "Alert" geändert wird.
    
    ![Dynamische Aktion konfigurieren](images/add-spatial-analysis-13.png)
    
6.  Ihre Kartenregion enthält derzeit eine Statusebene, in der alle Status angezeigt werden. Sie können diesen Layer jetzt so anpassen, dass nur der im Menü P3\_STATE ausgewählte Status angezeigt wird. Klicken Sie im Seitenbaum auf der linken Seite unter Ebenen auf Zustände. Ändern Sie in den Layer-Eigenschaften rechts unter Identifikation den Namen in **Ausgewählter Status**. Setzen Sie die Where-Klausel unter "Quelle" auf **state\_code = :P3\_STATE**. Beachten Sie im Seitenbaum auf der linken Seite, dass der Layer-Name in "Ausgewählter Status" geändert wird.
    
        <copy>
        state_code = :P3_STATE
        </copy>
        
    
    ![WHERE-Klausel konfigurieren](images/add-spatial-analysis-14.png)
    
7.  Schließlich aktualisieren Sie die Ebene "Flughäfen", um Artikel zurückzugeben, die nach dem benutzerdefinierten Status und der Nähe gefiltert sind. Klicken Sie in der Seitenstruktur auf der linken Seite auf die Ebene "Flughäfen". Ändern Sie in den Layer-Eigenschaften rechts unter "Quelle" den Typ in **SQL-Abfrage**. Geben Sie für SQL Query Folgendes ein, das den nativen SQL-Operator "innerhalb der Entfernung" von Oracle Database verwendet.
    
        <copy>
        select a.*
          from EBA_SAMPLE_MAP_AIRPORTS a,
               EBA_SAMPLE_MAP_SIMPLE_STATES b
         where b.state_code= :P3_STATE
           and a.land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance='|| :P3_DISTANCE ||' unit=KM') = 'TRUE'
        </copy>
        
    
    Geben Sie für die weiterzuleitenden Seitenelemente die durch Komma getrennte Liste **P3\_STATE,P3\_DISTANCE** ein.
    
    ![Räumliche SQL-Abfrage](images/add-spatial-analysis-15.png)
    
8.  Ihre Seite kann jetzt angezeigt werden. Klicken Sie auf **Save**, und klicken Sie dann oben rechts auf die grüne Schaltfläche **Run**. Nachdem die Seite wiedergegeben wurde, wählen Sie für den Status **Alabama** aus. Auf der Karte werden der ausgewählte Bundesstaat und die Flughäfen innerhalb von 100 km angezeigt (Standardentfernung).
    
    ![Seite speichern und ausführen](images/add-spatial-analysis-16.png)
    
9.  Ändern Sie den ausgewählten Status in **Kansas**. Beobachten Sie die Karte jetzt zeigt den ausgewählten Staat und Flughäfen mit 100 km.
    
    ![Kansas auswählen](images/add-spatial-analysis-17.png)
    
10.  Erhöhen Sie die Entfernung auf 600 km, und klicken Sie dann zum Weiterleiten auf Enter oder Tab. Beachten Sie, dass die Karte jetzt zusätzliche Flughäfen in größerer Entfernung anzeigt.
    
    ![Entfernung auf 600km erhöhen](images/add-spatial-analysis-18.png)
    
11.  Bestätigen Sie schließlich, dass die Weiterleitung einer negativen Entfernung zu dem zuvor konfigurierten Fehler-Popup führt.
    
    ![Alarm bei negativer Entfernung](images/add-spatial-analysis-19.png)
    
    Wie in der Sample Maps-Anwendung gezeigt, die Sie zu Beginn dieses Workshops installiert haben, gibt es eine enorme Menge an zusätzlichen Funktionen, die mit Map Regions und Spatial erreicht werden können. Dieser Workshop hat die Grundlagen eingeführt und wir hoffen, dass Ihr Interesse geweckt wurde und Sie die Leistungsfähigkeit von Karten und räumlichen Analysen in Ihren APEX-Anwendungen nutzen werden.
    

## Weitere Informationen

*   [Oracle Spatial](https://www.oracle.com/database/spatial/)
*   [APEX](https://apex.oracle.com/)

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, Database Product Management, März 2023