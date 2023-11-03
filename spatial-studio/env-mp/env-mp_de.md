# Spatial Studio installieren

## Einführung

In dieser Übung wird das Provisioning von Oracle Spatial Studio (Spatial Studio) mit dem Oracle Cloud Marketplace beschrieben. Der Oracle Cloud Marketplace bietet Apps und Services, die von Oracle und 3. Parteien bereitgestellt werden. Details finden Sie [hier](https://docs.oracle.com/en/cloud/marketplace/marketplace-cloud/index.html).

Geschätzte Laborzeit: 30 Minuten

### Ziele

In dieser Übung führen Sie folgende Schritte aus:

*   Erfahren Sie, wie Sie Spatial Studio über den Oracle Cloud Marketplace installieren
*   Erfahren Sie, wie Sie das Repository-Schema von Spatial Studio beim ersten Start festlegen

### Voraussetzungen

*   Free Tier-, Cloud-Account vom Typ "Immer kostenlos", "Kostenpflichtig" oder LiveLabs von Oracle
*   Repository-Schema erstellt (Übung 3).

## Aufgabe 1: Spatial Studio im Marketplace auswählen

1.  Klicken Sie auf das **Navigationsmenü** oben links, und wählen Sie **Marketplace** aus.

![Oracle Cloud Marketplace](https://oracle-livelabs.github.io/common/images/console/marketplace.png "Markt")

2.  Suchen Sie nach Spatial Studio, und klicken Sie auf die Oracle Spatial Studio-App

![Oracle Spatial Studio im Oracle Cloud Marketplace](images/env-marketplace-2.png "Oracle Spatial Studio Marketplace-Images")

3.  Prüfen Sie die Verwendungsanweisungen, akzeptieren Sie die Geschäftsbedingungen, und klicken Sie auf "Stack starten".

![Stack starten, um Oracle Spatial Studio bereitzustellen](images/env-marketplace-3.png "Stack starten")

## Aufgabe 2: Stack-Assistent erstellen

1.  Geben Sie optional einen benutzerdefinierten Namen und eine Beschreibung für den Deployment-Stack ein. Wählen Sie dann das Compartment aus, das für das Deployment verwendet werden soll, und klicken Sie auf "Weiter".

![Stackassistent erstellen](images/env-marketplace-4.png "Stack mit dem Assistenten erstellen")

2.  Wählen Sie Availability-Domain und Ausprägung für die Compute-Instanz aus.

Details zu Compute-Ausprägungen finden Sie [hier](https://docs.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm). Prüfen Sie in Availability-Domains auf Quota-Verfügbarkeit der gewünschten Ausprägung. Dies ist besonders wichtig, wenn Sie eine Ausprägung vom Typ "Immer kostenlos" verwenden: \*Navigieren Sie in der OCI-Konsole zu Governance > Limits, Quota und Nutzung \* Wählen Sie für den Service "Compute" und für den Geltungsbereich eine Availability-Domain aus \*Bestätigen Sie die Verfügbarkeit der gewünschten Ausprägung \* Ändern Sie gegebenenfalls die Auswahl der Availability-Domain, um die verfügbare Quota zu identifizieren

![Limits, Quota und Nutzung für Oracle Cloud-Ressourcen](images/env-marketplace-4-1.png "Limit für Compute-Ressourcen")

Nachdem die Quota bestätigt wurde, treffen Sie im Assistenten "Stack erstellen" eine Auswahl.

![Stackparameter festlegen](images/env-marketplace-5.png "Compute-Instanz auswählen")

Scrollen Sie dann nach unten.

3.  Ändern Sie optional den HTTPS-Port und den Admin-Benutzernamen von Spatial Studio von den Standardeinstellungen. Für die Authentifizierung des Spatial Studio-Admin-Benutzers haben Sie die Möglichkeit, OCI Vault Secrets oder ein Kennwort zu verwenden. Die Abbildung unten zeigt ein Beispiel mit einem Kennwort. Bei Produktions-Deployments wird empfohlen, OCI Vault Secrets zu verwenden. Scrollen Sie nach unten zum Abschnitt zur Netzwerkkonfiguration.

Hinweis: Standardmäßig ist der Spatial Studio-Admin-Benutzername **admin**. Dies ist ein Spatial Studio-Anwendungsbenutzer, der sich vom Datenbankbenutzernamen (studio\_repo) unterscheidet, der in Übung 3 für das in der Datenbank gespeicherte Repository-Schema erstellt wurde.

![Weitere Parameter wie Port und Kennwort festlegen](images/env-marketplace-6.png "Spatial Studio - Erweiterte Konfiguration - Administratorkennwort für Spatial Studio")

4.  Für Netzwerke haben Sie die Möglichkeit, automatisch ein neues oder ein vorhandenes VCN zu erstellen. Wählen Sie das Compartment aus, um ein neues VCN zu erstellen oder nach vorhandenen VCNs zu suchen.

Die Abbildung unten zeigt ein Beispiel mit "Neues VCN erstellen". Um ein vorhandenes VCN verwenden zu können, muss es sich in derselben Availability-Domain befinden wie oben in Schritt 2 ausgewählt. Wenn keine anderen VCNs vorhanden sind, können die restlichen Standardwerte unverändert beibehalten werden. Wenn andere VCNs vorhanden sind, aktualisieren Sie die CIDR-Werte, um Konflikte zu vermeiden.

![Netzwerk konfigurieren](images/env-marketplace-7.png "Erweiterte Spatial Studio-Konfiguration - Netzwerkkonfiguration")

Blättern Sie zum Abschnitt "SSH Keys".

5.  Durch das Laden eines SSH-Public Keys wird der Zugriff auf das Dateisystem von Spatial Studio zu administrativen Zwecken ermöglicht. Das Dialogfeld enthält Links zur allgemeinen SSH-Verbindungsdokumentation. Leiten Sie den SSH-Public Key weiter, indem Sie zur Schlüsseldatei navigieren oder die Schlüsselzeichenfolge kopieren und einfügen. Wenn Sie den SSH-Public Key aus einer Datei laden, wird der Name der Schlüsseldatei wie in der Abbildung unten dargestellt angezeigt. Klicken Sie auf "Next".

![SSH-Schlüssel hinzufügen](images/env-marketplace-8.png "Erweiterte Spatial Studio-Konfiguration - SSH-Public Key")

6.  Prüfen Sie die Übersicht Ihrer Einträge. Wenn Korrekturen erforderlich sind, klicken Sie auf "Zurück". Klicken Sie andernfalls auf {\\b Create}, um den Deployment-Prozess zu starten. Sie werden zu einer Seite mit Jobdetails für das Deployment umgeleitet.

![Stack erstellen](images/env-marketplace-9.png "Stackdefinition prüfen und Stack erstellen")

## Aufgabe 3: Deployment-Fortschritt überwachen

1.  Im Abschnitt "Logs" unten auf der Seite "Jobdetails" wird der Fortschritt angezeigt. Beim Einrichten für die Bereitstellung wird zunächst ein Drehfeld angezeigt.

![Stack-Deployment-Job überwachen - Terraform Apply](images/env-marketplace-10.png "Fortschritt des Stack-Deployments überwachen")

Nach einigen Minuten werden Protokollinformationen angezeigt.

![Loginformationen zum Deployment-Job](images/env-marketplace-11.png "Stack-Deployment-Log")

2.  Scrollen Sie nach unten zum Abschnitt "Logs". Nach Abschluss des Vorgangs werden "Apply Complete!" gefolgt von Instanzdetails angezeigt. Das letzte aufgelistete Element ist die öffentliche URL von Spatial Studio. Kopieren Sie diese URL, und fügen Sie sie in einen Browser ein.

![Deployment-Job erfolgreich abgeschlossen](images/env-marketplace-12.png "Ausgabevariablen für bereitgestellten Stack")

## Aufgabe 4: Erste Anmeldung

1.  Wenn Sie die öffentliche URL von Spatial Studio zum ersten Mal öffnen, wird eine Browserwarnung bezüglich Datenschutz und Sicherheit angezeigt. Die spezifische Warnung hängt von Ihrer Plattform und Ihrem Browser ab.

![Warnung beim Öffnen der Spatial Studio-URL](images/env-marketplace-13.png "Browser-Verbindungswarnung")

Dies ist kein Spatial Studio-Problem; es ist allgemein für den Zugriff auf Websites, die kein signiertes HTTPS-Zertifikat haben. Beim Laden und Konfigurieren eines signierten Zertifikats wird diese Warnung entfernt. Der Prozess des Ladens von Zertifikaten in Jetty ist jedoch außerhalb des Rahmens dieses Workshops.

Klicken Sie auf den Link, um zur Website zu gelangen.

2.  Geben Sie den Admin-Benutzernamen von Spatial Studio (Standard ist Admin) und das Kennwort ein, das Sie in Schritt 2 (Assistent zum Erstellen von Stacks, Element 3) eingegeben haben. Klicken Sie dann auf Anmelden.

![Benutzernamen und Kennwort für die Anmeldung bei Spatial Studio angeben](images/env-marketplace-14.png "Dialogfeld "Spatial Studio-Anmeldung"")

3.  Bei der ersten Anmeldung bei einer Spatial Studio-Instanz werden Sie zur Eingabe von Verbindungsinformationen für das Datenbankschema aufgefordert, das als Metadaten-Repository von Spatial Studio verwendet werden soll. Dies ist das Datenbankschema, das für alle Metadaten von Spatial Studio verwendet wird. Es kann auch von Spatial Studio-Administratoren zum Speichern anderer Daten verwendet werden. Sie verwenden das in Übung 3 erstellte Schema, wählen Sie also Oracle Autonomous Database aus, und klicken Sie auf "Next".

![Metadatenverbindungstyp auswählen](images/env-marketplace-15.png "Typ des Spatial Studio-Metadaten-Repositorys auswählen")

4.  Navigieren Sie zur in Übung 3 gespeicherten Wallet-Datei (oder verschieben Sie sie per Drag-and-Drop). Nach dem Laden wird der Wallet-Dateiname als ausgewähltes Wallet aufgeführt. Klicken Sie auf "OK".

![Wallet hochladen](images/env-marketplace-16.png "Verbindungs-Wallet hochladen")

5.  Geben Sie den in Übung 2 und dem Service definierten Benutzernamen und das Kennwort ein. Das mittlere Serviceniveau ist für diesen Workshop geeignet. Klicken Sie auf "OK".

![Verbindungsdetails für Metadaten-Repository eingeben](images/env-marketplace-17.png "Verbindungsdetails eingeben")

6.  Warten Sie einige Augenblicke, während Spatial Studio seine anfängliche Verbindung zum Schema herstellt und mehrere Metadatentabellen erstellt. Wenn Sie fertig sind, wird Spatial Studio mit Informationen zu den ersten Schritten geöffnet.

![Spatial Studio Homepage - Erste Schritte](images/env-marketplace-18.png "Landingpage für räumliches Studio")

## Aufgabe 5: Daten laden und Zuordnung erstellen

Um sicherzustellen, dass Spatial Studio ordnungsgemäß funktioniert, laden, vorbereiten und visualisieren Sie ein kleines Datenbeispiel. Die Daten enthalten eine Liste von Museen einschließlich Name und Adresse. Sie geocodieren die Daten und visualisieren sie auf einer interaktiven Karte.

1.  Hier wird keine Verbindung erstellt, da Sie für diese Verifizierung die Spatial Studio-Repository-Verbindung verwenden können. Klicken Sie auf die Kachel, um ein Dataset zu erstellen.

![Assistenten zum Hochladen von Daten starten](images/verify-1.png "Dataset erstellen")

2.  Laden Sie die Datenbeispieldatei [hier](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/sf_area_museums.xlsx) herunter, und speichern Sie sie an einem geeigneten Ort. Ziehen Sie die Datei dann per Drag-and-Drop in die Dateiuploadkachel. Sie können auch auf die Dateiuploadkachel klicken und zur Datei navigieren.

![Dataset durch Hochladen von Daten erstellen](images/verify-2.png "Vorhandene Tabellendaten hochladen")

3.  Legen Sie in der Datenvorschau die Uploadverbindung auf SPATIAL\_STUDIO fest, und setzen Sie den Datentyp für POSTAL\_CODE auf STRING. Klicken Sie dann auf **Weiterleiten**.

![Uploaddetails angeben](images/verify-3.png "Uploaddetails angeben und Spalteneinstellungen prüfen")

4.  Wenn der Upload abgeschlossen ist, wird das Dataset mit einem Warnsymbol aufgelistet, das angibt, dass Aktionen ausgeführt werden müssen. Klicken Sie auf das Warnsymbol und dann auf den Link **Gehe zu Datensetspalten**, um eine Schlüsselspalte zuzuweisen.

![Schlüsselspalte für das Dataset festlegen](images/verify-4.png "Dataset-Probleme lösen - Schlüsselspalte auswählen oder hinzufügen")

5.  Wählen Sie NAME als Schlüssel aus, und klicken Sie auf **Schlüssel validieren**.

![Schlüssel validieren](images/verify-5.png "Ausgewählten Schlüssel validieren")

Nachdem Sie den Schlüssel validiert haben, klicken Sie auf **Apply**.

6.  Klicken Sie erneut auf das Warnsymbol und dann auf die Schaltfläche **Geocode-Adressen**, um Adressen in Koordinatenpositionen für die Kartenvisualisierung zu konvertieren.

![Geocode-Adresse](images/verify-7.png "Dataset-Probleme lösen - Geocode-Adressen")

7.  Beachten Sie, dass die Spalten ADDRESS und POSTAL\_CODE automatisch zur Verwendung im Geocoding erkannt wurden. Übernehmen Sie die Standardwerte, und klicken Sie auf **Anwenden**.

![Zuordnung von Geocode-Adressen](images/verify-8.png "Dataset mit Geocoding-Referenzdaten zuordnen")

Wenn das Geocoding abgeschlossen ist, kehren Sie zur Seite "Datasets" zurück.

8.  Klicken Sie auf das Aktionsmenü für das Dataset SF\_AREA\_MUSEUMS, und wählen Sie **Projekt erstellen** aus.

![Mit der Erstellung des Projekts beginnen](images/verify-9.png "Neues Projekt für das Dataset erstellen")

9.  Klicken und ziehen Sie das Dataset SF\_AREA\_MUSEUMS, und legen Sie es an einer beliebigen Stelle auf der Karte ab.

![Datasets hinzufügen und auf die Kartenleinwand ziehen](images/verify-10.png "Datasets als Layer zum Projekt hinzufügen")

Das SF\_AREA\_MUSEUMS-Dataset wird als Kartenlayer hinzugefügt, und die Karte wird in den Bereich der Daten verschoben und vergrößert.

10.  Klicken Sie auf das Aktionsmenü für die Ebene SF\_AREA\_MUSEUMS, und wählen Sie **Einstellungen** aus.

![Datenlayer-Einstellungen](images/verify-11.png "Formate und mehr für die Datenebene definieren")

11.  Stylen Sie den Kartenlayer, indem Sie eine Farbe und Deckkraft Ihrer Wahl auswählen.

![Stileinstellung](images/verify-12.png "Farbe und Deckkraft für Datenlayer auswählen")

12.  Klicken Sie auf die Registerkarte **Interaktion**, aktivieren Sie **Infofenster anzeigen**, und wählen Sie alle Spalten aus. Klicken Sie dann auf ein Element in der Karte, um ein Informationsfenster mit den Datenwerten für das ausgewählte Element anzuzeigen.

![Einstellungen für Zuordnungsinteraktionen](images/verify-13.png "Details für die Interaktion mit der Karte definieren")

Dadurch wird sichergestellt, dass grundlegende Datenvorbereitung und -visualisierung ordnungsgemäß funktionieren.

13\. Klicken Sie auf den linken Navigationsbereich, um zur Seite "Datasets" zurückzukehren. Wählen Sie die Option **Änderungen verwerfen**, da dieser Test nicht beibehalten werden muss.

![Änderungen verwerfen](images/verify-14.png "Änderungen für das aktuelle Projekt verwerfen")

14.  Wenn die Verifizierung abgeschlossen ist, können Sie das Test-Dataset und die Datenbanktabelle löschen. Klicken Sie auf das Aktionsmenü für SF\_AREA\_MUSEUMS, und wählen Sie **Löschen** aus.

![Dataset löschen](images/verify-15.png "Dataset löschen")

15.  Wählen Sie die Option zum Löschen der Datenbanktabelle aus, und klicken Sie auf **OK**.

![Aktivieren Sie diese Option, um die Datenbanktabelle endgültig zu löschen](images/verify-16.png "Datenbanktabelle für das Dataset löschen")

Oracle Spatial Studio ist jetzt bereitgestellt und getestet. Die folgende Übung enthält Schritte zum Aufreißen von Spatial Studio, wenn es nicht mehr benötigt wird.

## Aufgabe 6: Spatial Studio deinstallieren (wenn nicht mehr benötigt)

**Wenn Sie Ihre Marketplace-Bereitstellung vollständig entfernen möchten, gehen Sie wie folgt vor.**

1.  Klicken Sie oben links auf das **Navigationsmenü**, navigieren Sie zu **Entwicklerservices**, und wählen Sie **Stacks** aus.

![Alle bereitgestellten Ressourcen bereinigen](https://oracle-livelabs.github.io/common/images/console/developer-resmgr-stacks.png "Marketplace-Bereitstellung entfernen")

2.  Wählen Sie das Compartment und den Namen aus, die in Schritt 2 verwendet werden. Im folgenden Beispiel wurde ein Compartment namens Sandbox und Stack namens Oracle Spatial Studio verwendet.

![Wählen Sie das richtige Compartment aus, und wählen Sie den zu löschenden Stack aus](images/env-marketplace-20.png "Stack auswählen")

3.  Wählen Sie "Terraform-Aktionen" > "Zerstören" aus

![Alle über den Oracle Spatial Studio-Stack bereitgestellten Ressourcen endgültig löschen](images/env-marketplace-21.png "Bereitgestellte Ressourcen zerstören")

Sie werden zur Bestätigung aufgefordert. Dadurch werden die Compute- und Netzwerkartefakte entfernt, die vom Marketplace-Deployment erstellt wurden.

4.  Nachdem Sie die Spatial Studio-App entfernt haben, bleibt das Repository-Schema unverändert. Um das Repository-Schema zu entfernen, melden Sie sich wie in Übung 3 als **admin** bei der Datenbank an, und führen Sie den folgenden Befehl aus.

    <copy>DROP USER studio_repo CASCADE;</copy>
    

## Weitere Informationen

*   [Spatial Studio-Produktseite](https://www.oracle.com/database/spatial/#rc30p2)
*   [Erste Schritte mit Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, Database Product Management, März 2023