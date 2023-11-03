# Mit RDF-Diagrammen in Graph Studio arbeiten

## Einführung

Mit Graph Studio in Oracle Autonomous Database können Benutzer Diagrammdaten modellieren, erstellen, abfragen und analysieren. Sie umfasst Notizbücher, Entwickler-APIs zur Ausführung von Diagrammabfragen mit PGQL, mehr als 60 integrierte Diagrammalgorithmen und bietet Dutzende von Visualisierungen, einschließlich nativer Diagrammvisualisierung. Zusätzlich zum Eigenschaftsdiagramm erweitert Graph Studio jetzt die Unterstützung für semantische Technologien, einschließlich Speicher-, Inferenz- und Abfragefunktionen für Daten und Ontologien basierend auf Resource Description Framework (RDF) und Web Ontology Language (OWL). Sie können jetzt Graph Studio für die folgenden unterstützten RDF-Features verwenden:

*   RDF-Graph erstellen
*   SPARQL-Abfragen im RDF-Diagramm in einem Notizbuchabsatz ausführen
*   RDF-Diagramme analysieren und visualisieren

RDF ist ein W3C-Standarddatenmodell zur Darstellung verknüpfter Daten. RDF verwendet URIs (Uniform Resource Identifier) als global eindeutige IDs für Ressourcen und URIs, um die Beziehung zwischen zwei Ressourcen zu benennen. Zusätzlich zu URIs verwendet RDF Literale, um skalare Werte wie Zahlen, Zeichenfolgen und Zeitstempel darzustellen. RDF-Modelle verknüpften Daten als gerichtete, beschriftete Grafik, wobei jede Kante normalerweise als Dreifach bezeichnet wird. Der Quellscheitel der Kante wird als Subjekt des Dreifachen bezeichnet. Das Label oder der Name der Kante wird als Prädikat des Dreifachen bezeichnet, und der Zielscheitel der Kante wird als Objekt des Dreifachen bezeichnet. RDF-Diagramme eignen sich besonders gut für Wissensdiagramme und Datenintegrationsanwendungen, da URIs global eindeutige IDs bereitstellen und die einfache, schemalose dreifache Struktur es sehr einfach macht, Daten aus mehreren verschiedenen RDF-Diagrammen in einem einzigen Diagramm zu kombinieren. Darüber hinaus bieten RDFS und OWL Standardmöglichkeiten zur Definition wiederverwendbarer Nomenklaturen (Sätze semantisch aussagekräftiger Kantenbezeichnungen und Ressourcentypen) für interoperabilere und maschinenverarbeitbare Diagrammdaten. Weitere Informationen zu den W3C RDF 1.1-Standards finden Sie [hier](https://www.w3.org/TR/rdf11-primer/).

SPARQL Protocol und RDF Query Language (SPARQL) sind eine der Technologien, die von der W3C für die Abfrage von Resource Description Framework-(RDF-)Daten standardisiert werden. Weitere Informationen zum Standard W3C SPARQL 1.1 finden Sie [hier](https://www.w3.org/TR/sparql11-overview/).

SPARQL verwendet eine **SELECT some elements WHERE some conditions**\-Struktur, um eine Abfrage anzugeben. Die Bedingungen in der WHERE-Klausel einer SPARQL-Abfrage werden mit dreifachen Mustern erstellt, die im Wesentlichen ein RDF-Dreifach sind, bei dem Elemente des Dreifachs durch Abfragevariablen ersetzt werden können (mit einem Präfix ? gekennzeichnet). Eine Abfragevariable in einem dreifachen Muster fungiert als Platzhalter. Betrachten Sie das dreifache Muster **?movie ms:genre ms:genre\_Comedy**. Wenn dieses dreifache Muster anhand eines RDF-Diagramms ausgewertet wird, werden alle **Subjekte** von Tripeln mit dem Prädikat **ms:genre** und **Objekt ms:genre\_Comedy** zurückgegeben. Die SPARQL SELECT-Klausel gibt eine Liste von Abfragevariablen an, die aus der Abfrage projiziert werden sollen. In der SPARQL-Syntax werden URIs in spitze Klammern eingeschlossen, und Literale werden in doppelte Anführungszeichen gesetzt (z. B. "Kevin Bacon"). Nach Literalen können ^^ und ein Datentyp-URI (z.B. "100"^^[http://www.w3.org/2001/XMLSchema#integer](http://www.w3.org/2001/XMLSchema#integer)) oder gefolgt von @ und einem Sprachtag (z.B. "Jalapeño"@es) folgen. Die meisten XML-Schemadatentypen werden in SPARQL unterstützt, und einfache Literale ohne Datentyp-URI werden als Datentyp [http://www.w3.org/2001/XMLSchema#string](http://www.w3.org/2001/XMLSchema#string) betrachtet.

Dieses Video unten ist ein Demo-Beispiel mit einem ähnlichen Datensatz, der in dieser Übung verwendet wird. Dieses Video betont die Struktur der Ontologie der Filmstruktur mit RDF. Die Demo bietet RDF Graph mit einer Staging-Tabelle in Kombination mit SQL Developer, die sich deutlich von dieser Autonomous Database-Version der Übung unterscheidet. Die SPARQL-Sprache, die zum Abfragen und Visualisieren der Daten verwendet wird, ist jedoch für den Kontext sehr ähnlich.

[](youtube:e_EQjInas50)

In dieser Übung wird ein semantisches Diagramm mit SPARQL erstellt, einer standardisierten Methode zur Integration verschiedener Datenquellen. In diesem Verfahren wird beschrieben, wie Sie die Daten mit grafikbasierten Abfragen und Visualisierungen analysieren.

Geschätzte Zeit: 35 Minuten

### Ziele

*   Umgebung vorbereiten
*   Erste Schritte mit RDF-Diagrammen
*   RDF-Graphbenutzer in Graph Studio erstellen und validieren
*   Abfragen und Visualisieren des RDF-Diagramms

### Voraussetzungen

In dieser Übung wird Folgendes vorausgesetzt:

*   Ein Oracle Cloud-Account - Auf der Landingpage LiveLabs dieses Workshops können Sie sehen, welche Umgebungen unterstützt werden

*   Laden Sie die MOVIESTREAM-Datei (moviestream\_rdf.nt) mit diesem [Link](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt) herunter

Damit endet diese Übung. Sie können jetzt _mit der nächsten Übung fortfahren._

## Danksagungen

*   **Autor** - Nicholas Cusato, Ethan Shmargad, Matthew McDaniel Solution Engineers, Ramu Murakami Gutierrez Produktmanager
*   **Technischer Mitarbeiter** - Melliyal Annamalai Distinguished Product Manager, Joao Paiva Consulting Mitglied des technischen Personals, Lavanya Jayapalan Principal User Assistance Developer
*   **Zuletzt aktualisiert am/um** - Ramu Murakami Gutierrez Product Manager, Juni 2023