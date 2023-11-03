# Compute-Instanz aus benutzerdefiniertem Image erstellen

## Einführung

Ein Compute-Image wurde vorab mit konfiguriertem Python erstellt. In dieser Übung erstellen Sie eine Compute-Instanz aus diesem Image.

Geschätzte Laborzeit: xx Minuten

### Ziele

*   Erstellen Sie eine Compute-Instanz aus einem benutzerdefinierten Image mit vorkonfiguriertem Python.

### Voraussetzungen

*   Abschluss der vorherigen Übung (Erstellen von SSH-Schlüsseln in Cloud Shell)

## Aufgabe 1: Compute-Instanz erstellen

1.  Navigieren Sie zu Compute > Instances. ![Compute-Instanzen](images/compute-01.png)
    
2.  Klicken Sie auf **Instanz erstellen** ![Instanzen erstellen](images/compute-02.png)
    
3.  Geben Sie einen Namen wie **my-compute** ein, oder übernehmen Sie den Standardwert. Wählen Sie ein Compartment aus, wenn Sie eines erstellt haben, oder übernehmen Sie den Standardwert (Root). Klicken Sie dann im Platzierungsabschnitt auf **Bearbeiten**. ![Instanzen erstellen](images/compute-03.png)
    
4.  If you plan to use Always Free resources, then select the availability domain that offers the **VM.Standard.E2.1.Micro** shape. ![Instanzen erstellen](images/compute-04.png)
    
5.  Scrollen Sie nach unten zum Abschnitt **Image und Ausprägung**, und klicken Sie auf **Bearbeiten**. ![Instanzen erstellen](images/compute-05.png)
    
6.  Klicken Sie auf **Image ändern**. ![Instanzen erstellen](images/compute-06.png)
    
7.  Wählen Sie **Meine Images** und **Image-OCID** aus ![Instanzen erstellen](images/compute-07.png)
    
8.  Kopieren Sie die folgende OCID, fügen Sie sie in das Feld "Image-OCID" ein, und klicken Sie auf **Image auswählen**.
    
        <copy>
         ocid1.image.oc1..aaaaaaaan727cclmzfl2evanaacnganaeobmv6hvakjzqdsk4gncmcklcxha
        </copy>
        
    
    ![Instanzen erstellen](images/compute-08.png)
    
9.  Scrollen Sie nach unten zum Abschnitt "Networking", und klicken Sie auf **Bearbeiten**. ![Instanzen erstellen](images/compute-09.png)
    
10.  Wenn Sie ein vorhandenes Netzwerk haben, können Sie es verwenden. Wählen Sie andernfalls **Neues virtuelles Cloud-Netzwerk erstellen** aus. Geben Sie für Namen **my-vcn** und **my-subnet** ein, oder übernehmen Sie die Standardwerte. Wählen Sie ein Compartment aus, wenn Sie eines erstellt haben, oder übernehmen Sie den Standardwert (Root). Bestätigen Sie unter der öffentlichen Adresse IPv4, dass **Öffentliche IPv4-Adresse zuweisen** ausgewählt ist. ![Instanzen erstellen](images/compute-10.png)
    
11.  Scrollen Sie nach unten zum Abschnitt **SSH-Schlüssel hinzufügen**, wählen Sie **Public Key einfügen** aus, und klicken Sie auf **Wiederherstellen**, um die Cloud Shell einzublenden. ![Instanzen erstellen](images/compute-11.png)
    
12.  Der letzte in Cloud Shell ausgeführte Befehl hat den Public Key gedruckt. Kopieren Sie den Public Key aus Cloud Shell, und fügen Sie ihn im Dialogfeld "Compute-Instanz erstellen" in das Feld "SSH-Schlüssel" ein. Blenden Sie dann die Cloud Shell aus. ![Instanzen erstellen](images/compute-12.png)
    
13.  Klicken Sie auf **Erstellen**. ![Instanzen erstellen](images/compute-13.png)
    
14.  Wenn das Provisioning abgeschlossen ist, kopieren Sie die öffentliche IP-Adresse der Compute-Instanz, und stellen Sie Cloud Shell wieder her. ![Instanzen erstellen](images/compute-14.png)
    
15.  Geben Sie den folgenden Befehl in Cloud Shell ein, um eine Verbindung zu Ihrer Compute-Instanz herzustellen. Dort können Sie "\[IP address\]" einfügen, das im vorherigen Schritt kopiert wurde.
    
        <copy>
         ssh -i ~/.ssh/my-ssh-key opc@[IP address]
        </copy>
        
    
    Wenn Sie aufgefordert werden, der Liste der bekannten Hosts hinzuzufügen, antworten Sie mit **yes**. ![Instanzen erstellen](images/compute-15.png)
    

Ihre Compute-Instanz wurde erstellt, und Sie haben den SSH-Zugriff geprüft.

## Aufgabe 2: Netzwerkport 8001 öffnen

1.  Wählen Sie im Hauptnavigationsbereich die Option **Networking**. Wählen Sie dann **Virtuelle Cloud-Netzwerke** aus. ![Instanzen erstellen](images/compute-16.png)
    
2.  Klicken Sie auf das in der vorherigen Aufgabe erstellte VCN. ![Instanzen erstellen](images/compute-17.png)
    
3.  Scrollen Sie nach unten, und klicken Sie links auf **Sicherheitslisten**. Klicken Sie dann auf **Standardsicherheitsliste für my-vcn**. ![Instanzen erstellen](images/compute-18.png)
    
4.  Klicken Sie auf **Ingress-Regeln hinzufügen**. ![Instanzen erstellen](images/compute-19.png)
    
5.  Geben Sie für das Quell-CIDR **0.0.0.0/0** ein. Geben Sie unter "Zielportbereich" **8001** ein. Klicken Sie dann auf **Ingress-Regel hinzufügen**. ![Instanzen erstellen](images/compute-20.png)
    
6.  Scrollen Sie nach unten, und beobachten Sie die neue Ingress-Regel, die eingehenden Zugriff auf Port 8001 ermöglicht. ![Instanzen erstellen](images/compute-21.png)
    

Sie können jetzt **mit der nächsten Übung fortfahren**.

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, Database Product Management, Juni 2023