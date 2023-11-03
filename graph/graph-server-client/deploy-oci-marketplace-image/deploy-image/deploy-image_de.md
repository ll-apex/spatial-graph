# Graph Server- und Client Marketplace-Image bereitstellen

## Einführung

In dieser Übung werden Sie durch die Schritte zum Bereitstellen und Konfigurieren des Graph Server- und Client-Kits auf einer Compute-Instanz über einen Oracle Cloud Marketplace-Stack geführt. Sie müssen während des Deployment-Prozesses den SSH-Schlüssel, die VCN- und Subnetzinformationen sowie die JDBC-URL für die ADB-Instanz angeben.

Geschätzte Zeit: 7 Minuten

### Ziele

*   Erfahren Sie, wie Sie das Graph Server- und Client-OCI Marketplace-Image bereitstellen.

### Voraussetzungen

*   SSH-Schlüssel für die Verbindung mit einer Compute-Instanz
*   Eine ADB-Instanz mit dem heruntergeladenen Wallet

## Aufgabe 1: Netzwerk für Graph Server erstellen

1.  Gehen Sie zu Oracle Cloud-Konsole > Networking > Virtuelle Cloud-Netzwerke
    
    ![Netzwerk-vcn](https://oracle-livelabs.github.io/common/images/console/networking-vcn.png)
    
2.  VCN-Assistenten starten > VCN mit Internetverbindung erstellen > VCN-Assistenten starten
    
    *   VCN-NAME: Beispiel: **vcn1**
    *   Die restlichen Elemente: Muss nicht geändert werden
3.  Sie müssen Port 7007 öffnen. Gehen Sie zu "Virtuelle Cloud-Netzwerke > vcn1 > Öffentliches Subnetz - vcn1 > Standardsicherheitsliste für vcn1 > Ingress-Regeln hinzufügen", und erstellen Sie die Regel unten:
    
    *   Quelltyp: **CIDR**
    *   Quell-CIDR: **0.0.0.0/0** (Diese Einstellung dient nur zum Testen. Bitte ersetzen Sie die IP-Adresse der Client-Rechner für den tatsächlichen Gebrauch.)
    *   IP-Protokoll: **TCP**
    *   Quellportbereich: **(Alle)**
    *   Zielportbereich: **7007**
    *   Beschreibung: z.B. **Für Graph Server**
    
    ![Ingress-Regel](images/ingress-rule.png)
    

## Aufgabe 2: Graph Server und Client im Marketplace suchen

Oracle Cloud Marketplace ist eine Onlineplattform, die Oracle- und Partnersoftware als Click-to-Deploy-Lösungen zur Erweiterung von Oracle Cloud-Produkten und -Services anbietet.

Oracle Cloud Marketplace-Stacks sind eine Reihe von Terraform-Vorlagen, die eine vollständig automatisierte End-to-End-Bereitstellung einer Partnerlösung auf Oracle Cloud Infrastructure bieten.

1.  Gehen Sie zu Ihrer Cloud-Konsole. Navigieren Sie zur Registerkarte **Marketplace**, und geben Sie "Graph Server and Client" in die Serach-Leiste ein. Klicken Sie auf den Oracle Graph Server and Client-Stack.
    
    ![Marktplatz](images/marketplace.png)
    
2.  Wählen Sie den Stack aus, und prüfen Sie dann die Systemvoraussetzungen und Verwendungsanweisungen. Wählen Sie dann die Version **22.4.x** (18-monatiges Patchrelease), wählen Sie ein Compartment aus, und klicken Sie auf **Stack starten**.
    
    ![Launch-Stack](images/launch-stack.png)
    
3.  **Stackinformationen**: Sie müssen keine Änderungen vornehmen. Fahren Sie mit **Weiter** fort.
    
    ![Create-Stack](images/create-stack.png)
    
4.  **Variablen konfigurieren**: Sie müssen folgende Optionen auswählen oder angeben:
    
    *   Oracle Graph Server-Ausprägung: Eine für immer kostenlose Ausprägung ist **VM.Standard.E2.1. Mikrobiologie**
    *   SSH-Public Key: Wird verwendet, wenn Sie später eine SSH-Verbindung zur bereitgestellten Instanz herstellen.
    
    ![configure-variables-1](images/configure-variables-1.png)
    
    *   Vorhandenes virtuelles Cloud-Netzwerk: Das oben erstellte Netzwerk, **vcn1**
    *   Vorhandenes Subnetz: Das oben erstellte Subnetz, **Öffentliches Subnetz-vcn1**
    *   JDBC-URL für Authentifizierung: **`JDBC:oracle:thin:@adb1_low?TNS_ADMIN=/etc/oracle/graph/wallets`**
    
    ![configure-variables-2](images/configure-variables-2.png)
    
    JDBC-URL oben:
    
    *   This is the TNS\_ADMIN entry points to the directory where you **will** have uploaded and unzipped the wallet **on the Compute instance** which will be created in this process
    *   Wenn Sie der Datenbank einen anderen Namen gegeben haben, z.B. **adb2**, ersetzen Sie **`@adb1_low`** in der JDBC-URL durch **`@adb2_low`**.
    *   Diese JDBC-URL wird in **/etc/oracle/graph/pgx.conf** gespeichert und kann bei Bedarf später aktualisiert werden
5.  Klicken Sie auf **Weiter**, um den Resource Manager-Job für den Stack zu initiieren. Der Job dauert 2-3 Minuten.
    
    ![rmj-1](images/rmj-1.png)
    
    Der Fortschritt wird in der Logausgabe angezeigt.
    
    ![rmj-2](images/rmj-2.png)
    
    Sobald der Job erfolgreich abgeschlossen wurde, ändert sich der Status von "In Bearbeitung" in "Erfolgreich". Wenn Sie die **Ausprägung VM.Standard.E2.1 erhalten. Fehler "Micro nicht gefunden"**. Die Availability-Domain kann die ausgewählte Ausprägung nicht angeben. Bearbeiten Sie den Job, ändern Sie die Availability-Domain, und versuchen Sie es erneut. (Eine immer kostenlose Compute-VM kann nur in Ihrer Hauptregion erstellt werden. Wenn Sie zuvor eine immer kostenlose Compute-VM erstellt haben, dann diese neue VM.Standard.E2.1. Mikroinstanz kann nur in derselben Availability-Domain wie die vorherige erstellt werden.)
    
    ![rmj-3](images/rmj-3.png)
    
    _**HINWEIS:**_ _Wenn Sie fertig sind, notieren Sie sich **public\_ip** und **graphviz\_public\_url**, damit Sie später in dieser Übung eine SSH-Verbindung zur ausgeführten Instanz herstellen und auf die Diagramm-Version zugreifen können._
    

## Aufgabe 3: ADB-Wallet herunterladen

1.  Gehen Sie zur Cloud-Konsole, und wählen Sie unter **Oracle Database** die Option **Autonomous Transaction Processing** aus. Wenn die Instanz nicht angezeigt wird, stellen Sie sicher, dass der **Workload-Typ** **Transaktionsverarbeitung** oder **Alle** lautet.
    
    ![datenbank-atp](https://oracle-livelabs.github.io/common/images/console/database-atp.png)
    
2.  Klicken Sie auf die Autonomous Database-Instanz. Klicken Sie auf der Seite "Autonomous Database-Details" auf **Datenbankverbindung**.
    
    ![Brieftasche-1](images/wallet-1.png)
    
3.  Wählen Sie im Fenster "Datenbankverbindung" als Wallet-Typ **Instance Wallet** aus, und klicken Sie auf **Wallet herunterladen**.
    
    ![Brieftasche-2](images/wallet-2.png)
    
4.  Geben Sie im Dialogfeld "Wallet herunterladen" ein (neues) Wallet-Kennwort in die Felder "Kennwort" ein. Dieses Kennwort schützt das heruntergeladene Wallet mit den Clientzugangsdaten.
    
    Klicken Sie auf **Download**, um die ZIP-Datei mit den Clientsicherheitszugangsdaten zu speichern. ![Brieftasche-3](images/wallet-3.png)
    
    Der Name lautet standardmäßig: **Wallet\_<database\_name>.zip**
    

Der Inhalt in diesem Abschnitt wird über [Clientzugangsdaten (Wallets) herunterladen](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/connect-download-wallet.html#GUID-B06202D2-0597-41AA-9481-3B174F75D4B1) angepasst

## Aufgabe 4: ADB-Wallet hochladen

In diesem Schritt benötigen Sie das Shell-Tool zum Ausführen von **scp**\- und **ssh**\-Befehlen, z.B. Oracle Cloud Shell, Terminal, wenn Sie MAC verwenden, oder Gitbash, wenn Sie Windows verwenden.

Kopieren Sie das Wallet von Ihrem lokalen Rechner in die Graph Server-Instanz auf OCI.

    <copy>
    scp -i <private_key> <Wallet_database_name>.zip opc@<public_ip_for_compute>:/etc/oracle/graph/wallets
    </copy>
    

Beispiel:

    <copy>
    scp -i key.pem ~/Downloads/Wallet_adb1.zip opc@203.0.113.14:/etc/oracle/graph/wallets
    </copy>
    

## Aufgabe 5: ADB-Wallet entpacken

1.  Stellen Sie als **opc**\-Benutzer mit dem zuvor erstellten Private Key eine SSH-Verbindung zur Compute-Instanz her.
    
        <copy>
        ssh -i <private_key> opc@<public_ip_for_compute>
        </copy>
        
    
    Beispiel:
    
        <copy>
        ssh -i key.pem opc@203.0.113.14
        </copy>
        
2.  Dekomprimieren Sie das ADB-Wallet in das Verzeichnis **/etc/oracle/graph/wallets/**, und ändern Sie die Gruppenberechtigung.
    
        <copy>
        cd /etc/oracle/graph/wallets/
        unzip Wallet_adb1.zip
        chgrp oraclegraph *
        </copy>
        
3.  Prüfen Sie optional, ob Sie den richtigen Servicenamen in der JDBC-URL verwendet haben, die Sie bei der Konfiguration des OCI-Stacks eingegeben haben.
    
        <copy>
        cat /etc/oracle/graph/wallets/tnsnames.ora
        </copy>
        
    
    Der Eintrag `adb1_low` wird wie folgt angezeigt:
    
        <copy>
        adb1_low =
            (description=
                (address=
                    (https_proxy=proxyhostname)(https_proxy_port=80)(protocol=tcps)(port=1521)
                    (host=adwc.example.oraclecloud.com)
                )
                (connect_data=(service_name=adwc1_low.adwc.oraclecloud.com))
                (security=(ssl_server_cert_dn="adwc.example.oraclecloud.com,OU=Oracle BMCS US,O=Oracle Corporation,L=Redwood City,ST=California,C=US"))
        )
        </copy>
        

Sie können jetzt mit der nächsten Übung fortfahren.

## Danksagungen

*   **Autor** - Jayant Sharma
*   **Mitwirkende** - Arabella Yao, Jenny Tsai
*   **Zuletzt aktualisiert am/um** - Ryota Yamanaka, März 2023