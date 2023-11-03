/\* DIESE DATEI IN DER NÄCHSTEN RELEASE LÖSCHEN - BITTE VERWENDEN SIE ADB-PROVISION-CONDITIONAL.MD DATEI INSTEAD UND SPEZIFIEREN SIE DIE VERSION, DIE SIE IN IHREM MANIFEST WOLLTEN: { "Titel": "Lab 1: Provisioning an ADB Instance", "Beschreibung": "Provisioning an Autonomous Database Instance", "Typ": "livelabs", "Dateiname": "https://oracle-livelabs.github.io/adb/shared/adb-provision/adb-provision-conditional.md" }, \*/

# Autonomous Database (ADW und ATP) bereitstellen

## Einführung

In dieser Übung werden die Schritte für die ersten Schritte mit Oracle Autonomous Database (Autonomous Data Warehouse \[ADW\] und Autonomous Transaction Processing \[ATP\]) in Oracle Cloud beschrieben. In dieser Übung stellen Sie eine neue ADW-Instanz bereit.

> **Hinweis:** Während diese Übung ADW verwendet, sind die Schritte zum Erstellen einer ATP-Datenbank identisch.

Voraussichtliche Zeit: 5 Minuten

### Ziele

*   Erfahren Sie, wie Sie eine neue Autonomous Database bereitstellen

## Aufgabe 1: ADW oder ATP im Menü "Services" auswählen

1.  Melden Sie sich bei Oracle Cloud an.
    
2.  Sobald Sie angemeldet sind, gelangen Sie zum Cloud-Service-Dashboard, in dem Sie alle für Sie verfügbaren Services anzeigen können. Klicken Sie oben links auf das Navigationsmenü, um Navigationsoptionen der obersten Ebene anzuzeigen.
    
    > **Hinweis:** Sie können auch direkt auf Ihren Autonomous Data Warehouse- oder Autonomous Transaction Processing-Service im Abschnitt **Schnellaktionen** des Dashboards zugreifen.
    
    ![Oracle-Homepage.](./images/Picture100-36.png " ")
    
3.  Die folgenden Schritte gelten gleichermaßen für Autonomous Data Warehouse oder Autonomous Transaction Processing. In dieser Übung wird das Provisioning einer Autonomous Data Warehouse-Datenbank angezeigt. Klicken Sie also auf **Autonomous Data Warehouse**.
    
    ![Klicken Sie auf "Autonomous Data Warehouse".](https://oracle-livelabs.github.io/common/images/console/database-adw.png " ")
    
4.  Stellen Sie sicher, dass der Workload-Typ **Data Warehouse** oder **Alle** lautet, um Ihre Autonomous Data Warehouse-Instanzen anzuzeigen. Verwenden Sie das Dropdown-Menü **Listengeltungsbereich**, um ein Compartment auszuwählen. Geben Sie den ersten Teil Ihres Benutzernamens ein. Beispiel: `LL185` im Feld "Compartments suchen", um Ihr Compartment schnell zu finden.
    
    ![Prüfen Sie den Workload-Typ auf der linken Seite.](images/livelabs-compartment.png " ")
    
5.  Diese Konsole zeigt an, dass noch keine Datenbanken vorhanden sind. Wenn eine lange Liste von Datenbanken vorhanden ist, können Sie die Liste nach dem **Status** der Datenbanken filtern (Verfügbar, Gestoppt, Beendet usw.). Sie können auch nach **Workload-Typ** sortieren. Hier ist der Workload-Typ **Data Warehouse** ausgewählt.
    
    ![Konsole für autonome Datenbanken.](./images/Compartment.png " ")
    

## Aufgabe 2: ADB-Instanz erstellen

1.  Klicken Sie auf **Autonomous Database erstellen**, um den Instanzerstellungsprozess zu starten.
    
    ![Klicken Sie auf "Create Autonomous Database".](./images/Picture100-23.png " ")
    
2.  Daraufhin wird der Bildschirm **Autonomous Database erstellen** angezeigt, in dem Sie die Konfiguration der Instanz angeben.
    
    ![](./images/create-adb-screen-livelabs-default.png " ")
    
3.  Geben Sie grundlegende Informationen für die autonome Datenbank an:
    
    *   **Compartment auswählen**: Behalten Sie das Standard-Compartment bei.
    *   **Anzeigename** - Geben Sie einen unvergesslichen Namen für die Datenbank zu Anzeigezwecken ein. Für diese Übung verwenden Sie **ADW Finance Mart**.
    *   **Datenbankname** - Verwenden Sie nur Buchstaben und Zahlen, beginnend mit einem Buchstaben. Die maximale Länge beträgt 14 Zeichen. (Unterstriche werden anfänglich nicht unterstützt.) Verwenden Sie für diese Übung **ADWFINANCE**, und **hängen Sie Ihre Benutzer-ID an**. Beispiel: Wenn Ihre Benutzer-ID **LL-185** lautet, geben Sie **ADWFINANCE185 ein.**
    
    ![Geben Sie Details ein.](./images/Picture100-26-livelabs.png " ")
    
4.  Wählen Sie einen Workload-Typ aus. Wählen Sie den Workload-Typ für die Datenbank aus:
    
    *   **Data Warehouse** - Wählen Sie in dieser Übung **Data Warehouse** als Workload-Typ aus.
    *   **Transaktionsverarbeitung** - Alternativ können Sie "Transaktionsverarbeitung" als Workload-Typ auswählen.
    
    ![Workload-Typ auswählen.](./images/Picture100-26b.png " ")
    
5.  Wählen Sie einen Deployment-Typ. Wählen Sie den Deployment-Typ für die Datenbank aus:
    
    *   **Gemeinsame Infrastruktur** - Wählen Sie für diese Übung die Option **Gemeinsame Infrastruktur** als Deployment-Typ aus.
    *   **Dedizierte Infrastruktur** - Alternativ können Sie "Dedizierte Infrastruktur" als Deployment-Typ auswählen.
    
    ![Wählen Sie einen Deployment-Typ aus.](./images/Picture100-26_deployment_type.png " ")
    
6.  Konfigurieren Sie die Datenbank:
    
    *   **Immer kostenlos** - Wenn Ihr Cloud-Account ein Account vom Typ "Immer kostenlos" ist, können Sie diese Option auswählen, um eine autonome Datenbank vom Typ "Immer kostenlos" zu erstellen. Eine immer kostenlose Datenbank verfügt über 1 CPU und 20 GB Speicher. Für diese Übung sollten Sie "Immer kostenlos" deaktiviert lassen.
    *   **Datenbankversion auswählen** - Wählen Sie eine der verfügbaren Datenbankversionen aus.
    *   **OCPU-Anzahl** - Anzahl der CPUs für Ihren Service. Geben Sie für diese Übung **1 CPU** an. Wenn Sie eine Datenbank vom Typ "Immer kostenlos" auswählen, ist sie mit 1 CPU ausgestattet.
    *   **Speicher (TB)** - Wählen Sie Ihre Speicherkapazität in Terabyte aus. In dieser Übung geben Sie **1 TB** Speicher an. Wenn Sie sich für eine Datenbank vom Typ "Immer kostenlos" entscheiden, werden 20 GB Speicher bereitgestellt.
    *   **Autoskalierung**: In dieser Übung aktivieren Sie Autoskalierung, damit das System automatisch bis zu dreimal mehr CPU- und I/O-Ressourcen verwenden kann, um den Workload-Bedarf zu decken.
    *   **Neue Datenbankvorschau** - Wenn ein Kontrollkästchen zur Vorschau einer neuen Datenbankversion verfügbar ist, wählen Sie es NICHT aus.
    
    > **Hinweis:** Sie können eine autonome Datenbank vom Typ "Immer kostenlos" nicht vertikal oder horizontal skalieren.
    
    ![Wählen Sie die übrigen Parameter aus.](./images/Picture100-26c.png " ")
    
7.  Administratorzugangsdaten erstellen:
    
    *   **Kennwort und Kennwort bestätigen**: Geben Sie das Kennwort für den ADMIN-Benutzer der Serviceinstanz an. Das Passwort muss die folgenden Anforderungen erfüllen:
    *   Das Kennwort muss zwischen 12 und 30 Zeichen umfassen und mindestens einen Großbuchstaben, einen Kleinbuchstaben und ein numerisches Zeichen enthalten.
    *   Das Kennwort kann nicht den Benutzernamen enthalten.
    *   Das Kennwort darf keine doppelten Anführungszeichen (") enthalten.
    *   Das Kennwort muss sich von den letzten 4 verwendeten Kennwörtern unterscheiden.
    *   Das Kennwort darf nicht mit einem Kennwort übereinstimmen, das vor weniger als 24 Stunden festgelegt wurde.
    *   Geben Sie das Kennwort erneut ein, um es zu bestätigen. Notieren Sie sich das Kennwort.
    
    ![Geben Sie das Kennwort und die Kennwortbestätigung ein.](./images/Picture100-26d.png " ")
    
8.  Netzwerkzugriff auswählen:
    
    *   Übernehmen Sie für diese Übung den Standardwert "Sicherer Zugriff von überall aus".
    *   Wenn Sie Traffic nur von den angegebenen IP-Adressen und VCNs zulassen möchten, bei denen der Zugriff auf die Datenbank von allen öffentlichen IPs oder VCNs blockiert wird, wählen Sie im Bereich "Netzwerkzugriff auswählen" die Option "Sicherer Zugriff nur von zulässigen IPs und VCNs" aus.
    *   Wenn Sie den Zugriff auf einen privaten Endpunkt in einem OCI-VCN einschränken möchten, wählen Sie im Bereich "Netzwerkzugriff auswählen" die Option "Nur Zugriff über privaten Endpunkt" aus.
    *   Wenn die Option "Gegenseitige TLS-(mTLS-)Authentifizierung erforderlich" ausgewählt ist, ist mTLS erforderlich, um Verbindungen zu Autonomous Database zu authentifizieren. Mit TLS-Verbindungen können Sie ohne Wallet eine Verbindung zu Autonomous Database herstellen, wenn Sie einen JDBC-Thin-Treiber mit JDK8 oder höher verwenden. Optionen zum Zulassen von TLS oder nur gegenseitige TLS-(mTLS-)Authentifizierung finden Sie in der [Dokumentation für Netzwerkoptionen](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/support-tls-mtls-authentication.html#GUID-3F3F1FA4-DD7D-4211-A1D3-A74ED35C0AF5).
    
    ![Wählen Sie den Netzwerkzugriff aus.](./images/Picture100-26e.png " ")
    
9.  Wählen Sie einen Lizenztyp aus. Wählen Sie für diese Übung die Option **Bring Your Own License (BYOL)** aus. Die beiden Lizenztypen sind:
    
    *   **Bring Your Own License (BYOL)** - Wählen Sie diesen Typ aus, wenn Ihre Organisation über vorhandene Datenbanklizenzen verfügt.
    *   **Lizenz inklusive**: Wählen Sie diesen Typ aus, wenn Sie neue Datenbanksoftwarelizenzen und den Datenbank-Cloud-Service abonnieren möchten.
    
    ![Klicken Sie auf "Create Autonomous Database".](./images/Picture100-27-byol.png " ")
    
10.  Geben Sie für diese Übung keine E-Mail-Adresse des Kontakts an. Im Feld "Kontakt-E-Mail" können Sie Personen auflisten, um Betriebshinweise und Ankündigungen sowie ungeplante Wartungsbenachrichtigungen zu erhalten.
    
    ![Geben Sie keine E-Mail-Adresse des Kontakts an.](images/contact-email-field.png)
    
11.  Klicken Sie auf **Autonomous Database erstellen**.
    
12.  Ihre Instanz beginnt mit dem Provisioning. In wenigen Minuten wechselt der Status von Provisioning zu Verfügbar. Jetzt ist Ihre Autonomous Data Warehouse-Datenbank einsatzbereit! Sehen Sie sich hier die Details Ihrer Instanz an, einschließlich Name, Datenbankversion, OCPU-Anzahl und Speichergröße.
    

    ![Database instance homepage.](./images/Picture100-32.png " ")
    

_Fortfahren Sie mit der nächsten Übung_.

## Sie möchten mehr erfahren?

Klicken Sie [hier](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3), um eine Dokumentation zum typischen Workflow für die Verwendung von Autonomous Data Warehouse zu erhalten.

## Danksagungen

*   **Autor** - Nilay Panchal, ADB-Produktmanagement
*   **Für die Cloud angepasst von** - Richard Green, Hauptentwickler, Datenbankbenutzerunterstützung
*   **Mitwirkende** - Oracle LiveLabs QS-Team (Jeffrey Malcolm Jr, Intern | Arabella Yao, Product Manager Intern)
*   **Zuletzt aktualisiert am/um** - Richard Green, Februar 2022