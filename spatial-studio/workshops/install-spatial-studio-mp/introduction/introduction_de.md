# Einführung

## Über diesen Workshop

In diesem Workshop stellen Sie Spatial Studio über den OCI Cloud Marketplace in Oracle Cloud bereit und bereiten ein Schema in Autonomous Database vor, das als Metadaten-Repository von Spatial Studio verwendet werden soll.

Geschätzte Workshop-Zeit: 60 Minuten

### Oracle Spatial Studio

Oracle Spatial Studio (Spatial Studio) ist eine Webanwendung, die Selfservice-Zugriff auf die räumlichen Funktionen von Oracle Database bietet. Während diese Funktionen in der Vergangenheit die Codierung und/oder Verwendung von 3rd-Party-Tools erfordern, ermöglicht Spatial Studio Business-Anwendern, räumliche Analysen und interaktive Webkarten mit Selfservice-GUIs zu erstellen und zu teilen.

![Alternativer Bildtext](./images/spatial-studio.png "Räumliches Studio")

Spatial Studio arbeitet mit räumlichen Daten in Oracle Database, d.h. mit Tabellen und Views, die den Geometriedatentyp von Oracle enthalten. Bei diesen Daten handelt es sich um bereits vorhandene räumliche Daten oder nicht räumliche Daten, die mit Spatial Studio erstellt werden, um Geometrien basierend auf Attributen hinzuzufügen.

Spatial Studio ist eine Java EE-Anwendung, die über den Oracle Cloud Marketplace in Oracle Cloud bereitgestellt werden kann. Spatial Studio kann auch manuell in Oracle WebLogic oder Jetty oder als in sich enthaltener, vorab bereitgestellter Schnellstart für Tests bereitgestellt werden.

Weitere Informationen finden Sie unter \[https://oracle.com/goto/spatialstudio\] (https://oracle.com/goto/spatialstudio)

### Ziele

*   Erfahren Sie, wie Sie ein Datenbankschema für das Metadaten-Repository von Spatial Studio erstellen und zuweisen
*   Erfahren Sie, wie Sie Spatial Studio mit dem Cloud Marketplace installieren
*   Erfahren Sie, wie Sie Spatial Studio deinstallieren, wenn es nicht mehr benötigt wird

### Voraussetzungen

*   Für diesen Workshop ist eine Oracle Autonomous Database erforderlich.
*   SQL Developer Web wird mit Autonomous Database bereitgestellt und auch zum Erstellen des Spatial Studio-Repository-Schemas verwendet.
*   Wenn Sie bereits Zugriff darauf haben, können Sie nach dieser Einführung mit der Übung 3 fortfahren.
*   Andernfalls sollten Sie mit Übung 1 fortfahren.
*   Es ist keine vorherige Erfahrung mit Oracle Spatial erforderlich.
*   Ein Oracle Cloud-Account - Auf der Landingpage LiveLabs dieses Workshops können Sie sehen, welche Umgebungen unterstützt werden

_Hinweis: Wenn Sie über ein **kostenloses Testkonto** verfügen, wird Ihr Account nach Ablauf der kostenlosen Testversion in einen Account vom Typ "**Immer kostenlos**" konvertiert. Sie können keine Free Tier-Workshops durchführen, es sei denn, die Umgebung vom Typ "Immer kostenlos" ist verfügbar. **[Klicken Sie hier, um die häufig gestellte Fragen zu Free Tier aufzurufen.](https://www.oracle.com/cloud/free/faq.html)**_

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, Database Product Management, Januar 2021