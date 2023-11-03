# Einführung

## Über diesen Workshop

In diesem Workshop lernen Sie das Mapping in Oracle APEX mit dem Feature "Region zuordnen" und Oracle Spatial kennen. Sie installieren und untersuchen eine vordefinierte Beispielanwendung mit vielen nützlichen Zuordnungsbeispielen. Sie erstellen dann Ihre eigene Anwendung mit und konfigurieren Zuordnungen sowohl mit einem Assistenten als auch von Grund auf neu.

Die Kartenregion ist ein natives APEX-Feature, das in APEX 21.1 eingeführt wurde und die Möglichkeit bietet, interaktive Karten mit räumlichen Daten aus Oracle Spatial, GeoJSON und Koordinaten zu konfigurieren. In diesem Workshop wird Oracle Spatial als räumliche Datenquelle verwendet, sodass sowohl raue räumliche Daten als auch räumliche Analyseergebnisse problemlos integriert werden können.

![Beispiel-Maps-App](./images/intro-01.png "Oracle Application Express - Beispielzuordnungsanwendung ")

Geschätzte Workshop-Zeit: 1 Stunde 15 Minuten

### Oracle Application Express (APEX) und Oracle Spatial

Oracle Application Express (APEX) und Oracle Spatial sind Features von Oracle Database, einschließlich der Services Autonomous Data Warehouse (ADW) und Autonomous Transaction Processing (ATP).

Oracle Application Express (APEX) ist eine Low-Code-Entwicklungsplattform, mit der Sie skalierbare, sichere Unternehmens-Apps mit erstklassigen Features entwickeln und überall bereitstellen können. Mehr auf der [Oracle APEX-Produkt-Homepage](https://apex.oracle.com)

Oracle Spatial besteht aus einer Reihe von Funktionen für die Verwaltung, Analyse und Verarbeitung von Geodaten in Oracle Database. Mit einem nativen räumlichen Datentyp und Analysevorgängen wird die standortbasierte Analyse Mainstream und Colocation mit allen anderen Datenbankvorgängen. Weitere Informationen finden Sie auf der [Oracle Spatial-Produkt-Homepage](https://www.oracle.com/database/spatial)

### Ziele

*   Beispiele für die APEX-Zuordnungsregion verstehen
*   Erfahren Sie, wie Sie den Zuordnungsbereich erstellen und konfigurieren
*   Erfahren Sie, wie Sie Standortanalysen in Oracle Spatial integrieren können

### Voraussetzungen

*   Oracle APEX 21.1+ ist erforderlich. Die Screenshots in diesem Workshop werden mit APEX 21.2 erstellt. Da wir generell die Verwendung der [neuesten Version von APEX](https://www.oracle.com/tools/downloads/apex-downloads/) empfehlen, erwarten wir gelegentlich kleine Unterschiede in der Benutzeroberfläche.
*   Grundlegende Erfahrung mit Oracle APEX wird empfohlen, ist jedoch nicht erforderlich. Sehen Sie sich bei Bedarf den folgenden einführenden APEX-Workshop LiveLabs an: [App basierend auf vorhandenen Tabellen für Oracle Autonomous Cloud Service erstellen](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=628).
*   Grundlegende Erfahrung mit Oracle Spatial wird empfohlen, ist jedoch nicht erforderlich. Sehen Sie sich bei Bedarf den folgenden einführenden LiveLabs Spatial-Workshop an: [Einführung in Oracle Spatial](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=736)

_Hinweis: Wenn Sie über ein **kostenloses Testkonto** verfügen, wird Ihr Account nach Ablauf der kostenlosen Testversion in einen Account vom Typ "**Immer kostenlos**" konvertiert. Sie können keine Free Tier-Workshops durchführen, es sei denn, die Umgebung vom Typ "Immer kostenlos" ist verfügbar. **[Klicken Sie hier, um die häufig gestellte Fragen zu Free Tier aufzurufen.](https://www.oracle.com/cloud/free/faq.html)**_

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Beitragende** - Jayson Hanes, APEX Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, März 2023