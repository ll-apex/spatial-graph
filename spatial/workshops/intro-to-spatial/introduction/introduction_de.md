# Einführung

## Oracle Spatial

Die Mission von Oracle ist es, Menschen dabei zu helfen, Daten auf neue Weise zu sehen, Erkenntnisse zu gewinnen und endlose Möglichkeiten zu erschließen. Bei der räumlichen Analyse geht es darum, komplexe Interaktionen basierend auf geografischen Beziehungen zu verstehen - Fragen zu beantworten, die darauf basieren, wo sich Menschen, Assets und Ressourcen befinden. Spatial Insights ermöglichen Ihnen einen besseren Kundenservice, die Optimierung Ihrer Belegschaft, die Suche nach Einzelhandels- und Distributionszentren, die Bewertung von Vertriebs- und Marketingkampagnen und mehr. Mit den räumlichen Angeboten von Oracle können Entwickler, Datenbankexperten und Analysten eine umfassende Suite von räumlichen Datenmanagement-, Analyse- und Visualisierungstools verwenden, um räumliche Analysen und Zuordnungen in Anwendungen auf einer Datenmanagementinfrastruktur der Unternehmensklasse zu integrieren - Oracle Database und Oracle Exadata. Innovative Technologien von Oracle Cloud und Oracle Autonomous Database, der branchenweit einzigen selbstverwaltenden, selbstsichernden und selbstreparierenden Datenbank, stehen räumlichen Anwendungen zur Verfügung.

Wie unten dargestellt, bieten die räumlichen Features von Oracle Database skalierbaren und performanten Speicher, Verarbeitung und Analyse sowohl einfacher als auch erweiterter räumlicher Datentypen. Darüber hinaus wird eine Reihe bereitstellbarer Java EE-Komponenten zur Unterstützung allgemeiner Mid-Tier-Services bereitgestellt.

![Bild-Alt-Text](./images/spatial-platform.png)

Weitere Informationen finden Sie unter \[https://oracle.com/goto/spatial\] (https://oracle.com/goto/spatial)

Geschätzte Workshop-Zeit: 60 Minuten

### Workshop - Überblick

In diesem Workshop erstellen, konfigurieren und analysieren Sie räumliche Daten. Sie erstellen und konfigurieren räumliche Tabellen für STORES, WAREHOUSES, REGIONS und TORNADO\_PATHS aus gängigen Formaten und führen dann räumliche Abfragen aus, um ihre Beziehungen basierend auf Nähe und Eindämmung zu untersuchen. Sie transformieren die Ergebnisse schließlich mit nativer JSON-Unterstützung in ADB für die Entwicklerintegration.

Die Fähigkeit, Informationen basierend auf dem Standort zu beziehen, z. B. Daten basierend auf räumlicher Nähe und Eindämmung, ist in unzähligen Szenarien äußerst wertvoll. Es ist kein vorhandener Schlüssel vorhanden, der Filialstandorte mit einem Lager verknüpft. Aber räumlich ermöglicht es, eine solche Beziehung basierend auf der Nähe zu bestimmen. Ebenso gibt es keine vorhandene Beziehung zwischen Filialstandorten und Regionen, z.B. Steuerregionen. Aber Spatial ermöglicht es, ihre Beziehung basierend auf Eindämmung zu bestimmen. Darüber hinaus ermöglicht Spatial standortbasierte Analysen wie die Zusammenfassung von Informationen basierend auf der Nähe, beispielsweise Verluste aufgrund von Tornados innerhalb einer Entfernung von einem Standort. Anstatt diese Analysen in einem separaten System auszuführen, können Sie die integrierten räumlichen Features von ADB nutzen.

In diesem Workshop sammeln Sie Erfahrungen mit allen oben genannten Fähigkeiten.

### Voraussetzungen

\- Ein Oracle Cloud-Account \- Für diesen Workshop ist Zugriff auf einen Oracle Database- und SQL-Client (d.h. SQL Developer, SQL Developer Web, SQL\*Plus) erforderlich. - Wenn Sie bereits Zugriff darauf haben, können Sie nach dieser Einführung den Abschnitt "Beispieldaten erstellen" überspringen. - Sonst gehen Sie zu den Abschnitten "Oracle Cloud Account", "Autonomous Database" und "SQL Developer Web". - Es ist keine vorherige Erfahrung mit Oracle Spatial erforderlich. - Ein Oracle Cloud-Account

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Beitragende** - Karin Patenge, Datenbankproduktmanagement, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, September 2022