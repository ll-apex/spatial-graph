# Umgebung vorbereiten

## Einführung

Oracle Autonomous Transaction Processing (ATP) ist ein vollständig verwalteter Oracle-Datenbankservice mit "selbstverwaltenden" Features auf Oracle Cloud Infrastructure (OCI). Als Best Practice wird empfohlen, einen Benutzer mit Berechtigungen zur Verwendung von Graph Studio zu erstellen.

Die folgende Übungsanleitung zeigt, wie Sie eine Verfügbarkeitsprüfung bereitstellen und einen Benutzer mit Berechtigungen für Graph Studio erstellen.

Geschätzte Zeit: 15 Minuten

### Ziele

*   Erstellen Sie Autonomous Database auf Oracle Cloud.

### Voraussetzungen

*   Webbrowser
*   Stellen Sie immer sicher, dass Sie sich in der richtigen Region und im richtigen Compartment befinden

## **Aufgabe 1:** Bei Oracle Cloud anmelden

1.  Melden Sie sich in Ihrem Browser bei Oracle Cloud an.

## **Aufgabe 2:** ATP bereitstellen

Stellen Sie die Autonomous Transaction Processing-Datenbank (ATP) mit den folgenden Schritten bereit. Alternativ kann ein Autonomous Data Warehouse (ADW) ähnlich verwendet werden.

1.  Wählen Sie oben rechts in der OCI-Konsole die zugewiesene Region aus.
    
2.  Wählen Sie links oben im Hamburger-Menü "Oracle Database" und dann "Autonomous Transaction Processing" aus.
    

![Bild, das zeigt, wo im Menü die Option für den Zugriff auf Autonomous Transaction Processing ausgewählt wird](./images/atp.png)

3.  Klicken Sie auf "Create Autonomous Database".

![Bild mit der Schaltfläche zum Erstellen einer autonomen Datenbank](./images/create-adb.png)

4.  Wählen Sie Ihr Compartment aus.
    
5.  Geben Sie einen eindeutigen Namen (vielleicht Ihren Namen) für die Anzeige und den Datenbanknamen ein. Der Anzeigename wird in der Konsolen-UI verwendet, um die Datenbank zu identifizieren.
    

![Bild mit dem Speicherort zur Eingabe eines eindeutigen Namens für die Datenbank](./images/unique-name.png)

6.  Stellen Sie sicher, dass der Workload-Typ "Transaktionsverarbeitung" ausgewählt ist.
    
7.  Geben Sie ein Kennwort ein. Der Benutzername ist immer ADMIN. (Hinweis: Merken Sie sich Ihr Kennwort.)
    

![Bild, das zeigt, wo Ihr Kennwort deklariert wird](./images/password.png)

8.  Klicken Sie unten auf "Create Autonomous Database".
    
    In der Konsole wird angezeigt, dass ATP bereitgestellt wird. Dieser Vorgang dauert etwa 2 oder 3 Minuten.
    
    Sie können den Status des Provisionings in der Anforderung prüfen.
    

![Bild, das zeigt, wo der Status der bereitgestellten Datenbank geprüft werden soll](./images/status.png)

Damit endet diese Übung. _Jetzt können Sie mit der nächsten Übung fortfahren._

## Danksagungen

*   **Autor** - Nicholas Cusato (Santa Monica Specialist Hub)
*   **Mitwirkende** - Nicholas Cusato (Santa Monica Specialist Hub)
*   **Zuletzt aktualisiert am/um** - Nicholas Cusato, Februar 2022