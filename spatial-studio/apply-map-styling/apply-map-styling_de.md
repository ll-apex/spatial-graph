# Zuordnungsformatierung anwenden

## Einführung

Mit Spatial Studio können Sie das "Look and Feel" und die Interaktivität Ihrer Kartenebenen anpassen. Das Styling eines Kartenlayer umfasst Optionen wie Farbe, Transparenz und bei Punkten Marker. Das Styling kann auch automatisch durch Datenwerte gesteuert werden ("datengesteuertes Styling"), so dass Farbe und/oder Markergröße auf Datenwerten basiert. So können Sie beispielsweise Vertriebsregionen mit Farben basierend auf dem Umsatz wiedergeben. Interaktivität bezieht sich auf das, was geschieht, wenn ein Benutzer auf ein Element in einem Kartenlayer klickt oder den Mauszeiger darüber bewegt. Dazu gehört die Anzeige einer QuickInfo und/oder das Öffnen eines Popup-Fensters mit Datenwerten für das Element. In dieser Übung untersuchen Sie einige dieser Styling- und Interaktivitätsfunktionen.

Geschätzte Laborzeit: 30 Minuten

### Ziele

*   Erläuterungen zu Rendering-Stilen
*   Verständnis von datengesteuertem Styling
*   Erfahren Sie, wie Sie Farbschemas verwenden
*   Erfahren Sie, wie Sie die Interaktivität von Kartenebenen konfigurieren

### Voraussetzungen

*   Übung 2: Projekt erstellen erfolgreich abgeschlossen

## Aufgabe 1: Navigieren Sie zur Formatierung

1.  Navigieren Sie im linken Fensterbereich zur Seite "Projekte". Öffnen Sie das Aktionsmenü für LiveLabs Spatial Intro, und wählen Sie **Öffnen** aus. ![Projekt öffnen](images/apply-styling-1.png)
    
2.  Um sich auf die ACCIDENTS-Ebene zu konzentrieren, schalten Sie die 2 Polizeiebenen in der Karte aus, indem Sie auf die Sichtbarkeitssteuerelemente klicken (d.h. blaue Augenballsymbole). ![Nicht verwendete Layer abschalten](images/apply-styling-4.png)
    
3.  Wie in der vorherigen Übung öffnen Sie das Aktionsmenü für ACCIDENTS, und wählen Sie **Einstellungen** aus.
    

## Aufgabe 2: Cluster-Stil anwenden

1.  Punktschichten wie ACCIDENTS können mit verschiedenen Renderstilen gerendert werden. Jeder Renderstil hat seine eigenen Einstellungen. Ändern Sie den Renderstil von Circle (Standard) in Cluster. ![Rendering-Stil von Kreis zu Cluster ändern](images/apply-styling-5.png)
    
2.  Die Karte zeigt nun ACCIDENTS mit Kreisen an, um zahlreiche Punkte in Bereichen zu repräsentieren. Die Clusterkreisgröße basiert auf der Anzahl der in jedem Bereich gruppierten Punkte. Sie können mit der Farbe und dem Stil der Textbeschriftungen experimentieren, die der Anzahl der Punkte in jedem Cluster entsprechen. ![Cluster-Stil beobachten und experimentieren](images/apply-styling-6.png) Beachten Sie, dass die Cluster beim Vergrößern (Drehen des Mausrads) in kleinere Cluster explodieren und beim Verkleinern umgekehrt. ![Cluster-Stil beobachten und experimentieren](images/apply-styling-7.png)
    

## Aufgabe 3: Heatmap-Stil anwenden

1.  Ändern Sie den Render-Stil von Cluster in Heatmap. Die Karte gibt nun ACCIDENTS mit kontinuierlichen Farben basierend auf der Konzentration der Punkte wieder. Heiße Farben stellen die Konzentration von Punkten dar, und kühle Farben stellen die Dünnheit von Punkten dar. Ein Schlüsselparameter des Heatmap-Stils ist "Radius", der den Abstand um jeden Punkt zur Definition einer Konzentration steuert. Der Standardradius ist so groß, dass die anfängliche Heatmap nur Punktkonzentrationen entlang der Straßen anzeigt, was nicht sehr hilfreich ist. ![Rendering-Stil von Cluster zu Heatmap ändern](images/apply-styling-8.png) Um unsere Heatmap auf lokalisiertere Konzentrationen zu konzentrieren, reduzieren Sie den Radius von der Standardeinstellung auf 10 und beobachten Sie eine lokalisiertere Ansicht der Punktkonzentrationen. ![Radius von Standard auf 10 reduzieren](images/apply-styling-9.png)

## Aufgabe 4: Datengesteuerten Stil anwenden

1.  Ändern Sie den Render-Stil von Heatmap in Circle. Bei Verwendung des Kreis-Renderstils können Radius und Farbe durch Datenwerte gesteuert werden. Blenden Sie das Menü Farbe ein, und wählen Sie "Basierend auf Daten". ![Renderstil von Heatmap in Kreis ändern und Farbe in datengesteuerte ändern](images/apply-styling-10.png)
    
2.  Sie wählen nun die Spalte aus, die zur Steuerung der Formatierung verwendet werden soll. Wählen Sie die Spalte NR\_VEHICLES (d.h. Anzahl der am Unfall beteiligten Fahrzeuge) und beobachten Sie, wie die ACCIDENTS farbcodiert werden. Sie können die anderen Standardwerte übernehmen und dann oben im Bereich "Formatdetails" auf den Link **Zurück** klicken. ![Farbe in datengesteuerte ändern](images/apply-styling-11.png)
    
3.  Nachdem Sie nun Farben basierend auf Datenwerten zugewiesen haben, schließen Sie den Stil ab, indem Sie den Radius auf 3 und die Deckkraft auf 90% setzen. Aktualisieren Sie auch die Strichwerte (d.h. Gliederungswerte): Setzen Sie "Breite" auf 0,5, "Farbe" auf "Grau" und "Deckkraft" auf 90%. Sie können natürlich Ihre eigenen Werte für diese auswählen, wenn Sie es bevorzugen. Klicken Sie dann auf den Link **Zurück**, um zur Ebenenliste zurückzukehren. ![Heatmap stilisieren](images/apply-styling-12.png)
    

## Aufgabe 5: Symbolstil anwenden

1.  Als Nächstes verwenden Sie die verbleibende Punktstiloption "Symbol" für die Schicht POLICE\_POINTS. Aktivieren Sie die Ebene POLICE\_POINTS, und deaktivieren Sie die anderen 2 Ebenen in der Karte, indem Sie auf die Sichtbarkeitssteuerelemente (d.h. Augenballsymbole) klicken. Öffnen Sie das Aktionsmenü für POLICE\_POINTS, und wählen Sie **Einstellungen** aus.
    
    Ändern Sie "Render-Stil" in "Symbol", und klicken Sie dann in das Textfeld "Bild", um das Dialogfeld "Symbolauswahl" zu öffnen. Wählen Sie **Marker** aus, und aktualisieren Sie die Deckkraft auf 90% und den Größenfaktor auf 0,6. Sie können natürlich Ihre eigenen Werte für diese auswählen, wenn Sie es bevorzugen. Klicken Sie dann auf den Link **Zurück**, um zur Ebenenliste zurückzukehren. ![Render-Stil zu Symbol ändern](images/apply-styling-13.png)
    

## Aufgabe 6: Interaktivität anwenden

1.  Klicken Sie auf das Hamburger-Symbol für den Layer POLICE\_BOUNDS, und wählen Sie **Einstellungen** aus. Wählen Sie im Pulldown-Menü "Konfigurieren" die Registerkarte **Interaktion**. Die erste Art der Interaktivität, die wir für einen Layer konfigurieren, ist die Möglichkeit, ein Element(e) auszuwählen. Auswahlen werden für Analysen verwendet, z.B. wenn Sie die Elemente identifizieren möchten, die in einer ausgewählten Region enthalten sind. Standardmäßig ist die auswählbare Option aktiviert. Klicken Sie in POLICE\_BOUNDS-Bereiche, und beobachten Sie die hervorgehobene Auswahl.
    
    ![Bereiche in einem Layer wählbar machen](images/apply-interactions-1.png)
    
2.  Als Nächstes konfigurieren Sie QuickInfos, d.h. ein Popup, das angezeigt wird, wenn Sie mit der Maus auf ein Element zeigen. QuickInfos sind standardmäßig deaktiviert. Bewegen Sie den Mauszeiger über eine POLICE\_BOUNDS-Region, und beobachten Sie, dass nichts passiert. Aktivieren Sie dann im Bereich "Einstellungen" die Option **QuickInfo anzeigen**, wählen Sie eine QuickInfo-Spalte aus, zeigen Sie mit der Maus auf einen Bereich, und beobachten Sie die QuickInfo.
    
    ![QuickInfos konfigurieren](images/apply-interactions-2.png)
    
3.  Schließlich konfigurieren Sie das Infofenster, d.h. ein Popup, das beim Klicken auf ein Element angezeigt wird. Standardmäßig ist diese Option deaktiviert. Klicken Sie in einen POLICE\_BOUNDS-Bereich, und beobachten Sie, dass kein Informationsfenster angezeigt wird. Aktivieren Sie dann das **Infofenster anzeigen**, wählen Sie die anzuzeigenden Spalten aus, klicken Sie in einen POLICE\_BOUNDS-Bereich, und beobachten Sie das angezeigte Infofenster.
    

!["Info anzeigen" konfigurieren](images/apply-interactions-3.png)

## Aufgabe 7: Änderungen speichern

1.  Klicken Sie auf **Zurück** und dann auf **Speichern**, um das Projekt mit den Stiländerungen zu speichern. ![Speichern Sie die Änderungen](images/apply-styling-14.png)
    
2.  Kehren Sie zur Seite "Projekt" zurück, und beobachten Sie, wie die Miniaturansicht mit Änderungen aktualisiert wird. ![Speichern Sie die Änderungen](images/apply-styling-15.png)
    
3.  Klicken Sie auf das Hamburger-Symbol für das Projekt, und wählen Sie **Open** (oder klicken Sie auf die Projekt-Thumbnail), um zum Projekt zurückzukehren.
    

Sie können jetzt [mit der nächsten Übung fortfahren](#next).

## Weitere Informationen

*   \[Produktportal für Spatial Studio\] (https://oracle.com/goto/spatialstudio)

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - Denise Myrick, Database Product Management, April 2023