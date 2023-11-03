# Mit Graph Analytics Filme empfehlen

## Einführung

In diesem Workshop verwenden Sie Graph Studio, um Kundengemeinschaften basierend auf dem Filmansichtsverhalten zu erkennen und zu erstellen. Sobald Sie Gemeinschaften erstellt haben, geben Sie Empfehlungen basierend auf dem, was Ihre Community-Mitglieder beobachtet haben.

Geschätzte Zeit: 60 Minuten

### Informationen zu Graph Studio

Oracle Autonomous Database verfügt über Funktionen, mit denen es als skalierbare Eigenschaftsdiagrammdatenbank fungieren kann. Sie automatisieren die Erstellung von Diagrammmodellen und In-Memory-Diagrammen aus Datenbanktabellen. Sie umfassen Notizbücher und Entwickler-APIs für die Ausführung von Diagrammabfragen mit PGQL, einer SQL-ähnlichen Graphabfragesprache und über 60 integrierte Graphalgorithmen sowie viele Visualisierungen einschließlich nativer Graphvisualisierung.

Sehen Sie sich das folgende Video an, das eine Einführung in Eigenschaftsdiagramme und deren Anwendungsfälle gibt.

Graphanalyse mit Autonomous Database vereinfachen

[](youtube:eCd-969hrak)

In diesem Workshop verwenden Sie ein Diagramm, das aus den Tabellen MOVIE, CUSTOMER\_PROMOTIONS und CUSTSALES\_PROMOTIONS erstellt wurde. MOVIE und CUSTOMER\_PROMOTIONS sind Scheiteltabellen (jede Zeile in diesen Tabellen wird zu einem Scheitelpunkt). CUSTSALES\_PROMOTIONS verbindet die beiden Tabellen und ist die Edge-Tabelle. Jedes Mal, wenn ein Kunde in CUSTOMER\_PROMOTIONS einen Film in der Tabelle MOVIE mietet, das ist ein Rand im Diagramm. Dieses Diagramm wurde für Sie zur Verwendung in diesem Workshop erstellt.

Bei der Analyse eines Diagramms können Sie zwischen über 60 vordefinierten Algorithmen wählen. In diesem Workshop verwenden Sie den **personalisierten SALSA**\-Algorithmus, der eine gute Wahl für Produktempfehlungen ist. Kundenscheitel werden _Hubs_ zugeordnet, und Filme werden _Autoritäten_ zugeordnet. Höhere Hubscores weisen auf eine engere Beziehung zwischen Kunden hin. Höhere Autoritätswerte zeigen, dass der Scheitelpunkt (oder Film) eine wichtigere Rolle bei der Feststellung dieser Nähe spielt.

### Ziele

In diesem Workshop verwenden Sie die Graph Studio-Funktion von Autonomous Database, um:

*   Notizbuch verwenden
*   Einige PGQL-Diagrammabfragen ausführen
*   Verwenden Sie python, um personalisierte SALSA aus der Algorithmusbibliothek auszuführen
*   Abfragen und Speichern von Empfehlungen

### Voraussetzungen

*   Oracle Cloud-Account

## Danksagungen

*   **Autor** - Melli Annamalai, Produktmanager, Oracle Spatial and Graph
*   **Mitwirkende** - Jayant Sharma
*   **Zuletzt aktualisiert am/um** - Ramu Murakami Gutierrez, Produktmanager, Oracle Spatial and Graph, Februar 2023