# Auf Spatial Studio zugreifen

## Einführung

In dieser Übung wird der Zugriff auf Oracle Spatial Studio (Spatial Studio) über eine Oracle LiveLabs-Reservierung beschrieben. Ihre Umgebung umfasst Spatial Studio und eine Autonomous Database. Bei der ersten Anmeldung bei Spatial Studio geben Sie Verbindungsinformationen für Autonomous Database an.

Geschätzte Laborzeit: 10 Minuten

### Ziele

In dieser Übung führen Sie folgende Schritte aus:

*   Cloud Wallet für Autonomous Database herunterladen
*   1\. Mal bei Spatial Studio anmelden, um Autonomous Database-Verbindungsinformationen bereitzustellen

### Voraussetzungen

*   Eine abgeschlossene LiveLabs-Reservierung für "Einführung in Oracle Spatial Studio"

## Aufgabe 1: Cloud Wallet für Autonomous Database herunterladen

1.  Notieren Sie sich in den Workshop-Details Ihren Cloud-Benutzernamen, Ihr Kennwort, Ihr Compartment und Ihre Spatial Studio-IP-Adresse. Starten Sie dann die Cloud-Konsole.

![Alternativer Bildtext](images/1-1.png "Bildtitel")

2.  Melden Sie sich mit Ihrem Cloud-Benutzernamen und anfänglichen Kennwort mit **Oracle Cloud Infrastructure Direct Sign-in** an. Sie werden aufgefordert, das Standardpasswort zu ändern.

![Alternativer Bildtext](images/1-2.png "Bildtitel")

3.  Navigieren Sie zu **Oracle Database**, **Autonomous Database**.

![Alternativer Bildtext](images/1-3.png "Bildtitel")

4.  Geben Sie im Formular "Compartment" auf der linken Seite den zuvor angegebenen Compartment-Namen ein. Dadurch wird die Compartmentsliste dynamisch gefiltert. Wählen Sie nach der Liste Ihr Compartment aus. Daraufhin wird Autonomous Database aufgelistet. Klicken Sie auf den Link zu Autonomous Database.

![Alternativer Bildtext](images/1-4.png "Bildtitel")

5.  Klicken Sie auf **Datenbankverbindung** und dann auf **Wallet herunterladen**. Sie werden für ein Wallet-Kennwort hochgestuft. Geben Sie eine Zeichenfolge ein, da dieses Kennwort nicht verwendet wird. Speichern Sie die Brieftasche an einem bequemen Ort auf Ihrem Laptop, wie Sie sie im nächsten Schritt verwenden werden.

![Alternativer Bildtext](images/1-5.png "Bildtitel")

## Aufgabe 2: Spatial Studio - Erstanmeldung

1.  Sie verwenden jetzt die IP-Adresse von Spatial Studio, die Sie zuvor notiert haben. Öffnen Sie einen neuen Tab in Ihrem Browser, und navigieren Sie zu **https://\[Ihre IP-Adresse von Spatial Studio\]:4040/spatialstudio**. Beispiel: Wenn Ihre Spatial Studio-IP-Adresse 123.123.12.123 lautet, navigieren Sie zu https://123.123.12.123:4040/spatialstudio.. Da Ihre Spatial Studio-Instanz nicht mit einem signierten SSL-Zertifikat konfiguriert ist, wird eine browserspezifische Sicherheitswarnung angezeigt. Akzeptieren Sie die Warnung, und fahren Sie mit der Website fort. In einer Produktionsumgebung würde ein Zertifikat konfiguriert und dies würde nicht geschehen. Melden Sie sich mit dem Benutzer **admin** und dem Passwort **welcome1** an.

![Alternativer Bildtext](images/2-1.png "Bildtitel")

2.  Bei der ersten Anmeldung bei Spatial Studio werden Sie aufgefordert, Datenbankverbindungsinformationen für das Metadaten-Repository von Spatial Studio einzugeben. Klicken Sie auf **Autonomous Database** und dann auf **Weiter**. Ziehen Sie beim nächsten Scren die zuvor heruntergeladene Wallet-Datei per Drag-and-Drop, und klicken Sie auf **OK**.

![Alternativer Bildtext](images/2-2.png "Bildtitel")

3.  Sie werden jetzt zur Eingabe von Informationen zur automatisierten Datenbankverbindung aufgefordert. Geben Sie den Benutzer **studio\_repo**, das Kennwort **Welcome1Welcome1** ein, und wählen Sie den mittleren Servicegrad aus.

![Alternativer Bildtext](images/2-3.png "Bildtitel")

Spatial Studio erstellt jetzt seine Metadatentabellen in Autonomous Database. Dies dauert etwa 30 Sekunden.

4.  Wenn Spatial Studio geöffnet wird, ist die erste Anmeldung abgeschlossen und Sie können mit dem Workshop fortfahren.

![Alternativer Bildtext](images/2-4.png "Bildtitel")

Sie können jetzt [mit der nächsten Übung fortfahren](#next).

## Weitere Informationen

*   [Spatial Studio-Produktseite](https://oracle.com/goto/spatialstudio)

## Danksagungen

*   **Autor** - David Lapp, Database Product Management
*   **Zuletzt aktualisiert am/um** - David Lapp, Database Product Management, Juni 2021