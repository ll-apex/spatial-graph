# Verbindung zu Compute herstellen

## Einführung

Für den Zugriff auf den Python-Host-Compute benötigen Sie ein SSH-Schlüsselpaar. Oracle Cloud Infrastructure (OCI) Cloud Shell ist ein webbrowserbasiertes Terminal, auf das über die Oracle Cloud-Konsole zugegriffen werden kann und das Zugriff auf eine Linux-Shell bietet. Sie rufen ein SSH-Schlüsselpaar ab und stellen eine Verbindung zu Ihrem Python-Host in OCI Cloud Shell her.

Geschätzte Laborzeit: 5 Minuten

Sehen Sie sich das Video unten an, um einen schnellen Durchgang des Labors zu erhalten. [Übung 1](videohub:1_0tvxm2q0)

### Ziele

*   Compute-IP-Adresse abrufen
*   SSH-Schlüsselpaar abrufen
*   SSH-Verbindung zu Compute erstellen

### Voraussetzungen

*   Sie müssen bei der OCI-Konsole angemeldet sein

## Aufgabe 1: IP-Adresse der Compute-Instanz abrufen

1.  Navigieren Sie vom Hauptmenü zu Compute > Instances

![Cloud Shell öffnen](images/compute-01.png)

2.  Klicken Sie auf der Seite mit den Workshop-Anweisungen oben links auf **Anmeldeinformationen anzeigen**, und kopieren Sie Ihren Compartment-Namen.

![Cloud Shell öffnen](images/compartment.png)

1.  Fügen Sie in der OCI-Konsole Ihren Compartment-Namen ein, und wählen Sie ihn im Pulldown-Menü aus.

![Cloud Shell öffnen](images/compute-02.png)

4.  Notieren Sie sich die öffentliche IP der Compute-Instanz. Sie werden dies später in dieser und anderen Übungen verwenden.

![Cloud Shell öffnen](images/compute-03.png)

## Aufgabe 2: SSH-Schlüssel abrufen

1.  Öffnen Sie cloud shell.
    
    ![Cloud Shell öffnen](images/compute-04.png)
    
2.  Wenn Sie zur Ausführung des Tutorials aufgefordert werden, geben Sie N ein, und drücken Sie die Eingabetaste.
    
    ![Cloud Shell öffnen](images/compute-05.png)
    
3.  Führen Sie in der Befehlszeile jeden der folgenden Schritte aus, um Ihren SSH-Ordner zu erstellen und zu navigieren.
    
        <copy>
        mkdir ~/.ssh
        </copy>
        
    
          ```
        cd ~/.ssh "\`

![Schlüssel erstellen](images/compute-06.png)

1.  Führen Sie in der Befehlszeile den folgenden Befehl aus, um eine ZIP-Datei mit SSH-Schlüsseln abzurufen und aufzulisten.
    
        <copy>
        wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/hfpJ4-8XrB5tWBDUWvgnCmGch_1WHhihBrRpHNIzj6JSq5O5hbwp2wsqRPYbg8Gm/n/c4u04/b/livelabsfiles/o/labfiles/ocw23-keys.zip
        </copy>
        
    
        <copy>
        ls
        </copy>
        
    
    ![Schlüssel erstellen](images/compute-07.png)
    
2.  Um den Inhalt der ZIP-Datei zu dekomprimieren und aufzulisten, führen Sie in der Befehlszeile den folgenden Befehl aus:
    
        <copy>
        unzip ocw23-keys
        </copy>
        
    
        <copy>
        ls
        </copy>
        

![Schlüssel erstellen](images/compute-08.png)

## Aufgabe 3: Verbindung zur Compute-Instanz herstellen

2.  Führen Sie in der Befehlszeile den folgenden Befehl aus, um eine Verbindung zur Python-Compute-Instanz herzustellen. Dabei ist die IP-Adresse die Compute-IP-Adresse aus Aufgabe 1.
    
        <copy>
         ssh -i ~/.ssh/ocw23-rsa opc@[IP address]
        </copy>
        
    
    Wenn Sie aufgefordert werden, der Liste der bekannten Hosts hinzuzufügen, antworten Sie mit **yes**.
    
    ![Schlüssel erstellen](images/compute-09.png)
    
3.  Klicken Sie auf das Symbol "Ausblenden", um Cloud Shell zu minimieren.
    
    ![Cloud Shell ausblenden](images/compute-10.png)
    
4.  Beobachten Sie die Schaltfläche "Wiederherstellen", um Cloud Shell erneut zu öffnen. Cloud Shell wird in einer nachfolgenden Übung erneut geöffnet.
    
    ![Cloud Shell wiederherstellen](images/compute-11.png)
    

Sie können jetzt **mit der nächsten Übung fortfahren**.

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Mitwirkende** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Zuletzt aktualisiert am/um** - David Lapp, August 2023