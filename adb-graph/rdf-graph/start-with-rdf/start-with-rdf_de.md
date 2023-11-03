# Erste Schritte mit RDF-Diagrammen

## Einführung

In dieser Übung werden die ersten Schritte erläutert, indem Sie die RDF-Daten in einen Bucket hochladen, der mit Autonomous Database verknüpft wird. Dazu muss der korrekte OCI-Benutzername aus dem Profil kopiert werden. Damit Graph Studio auf die RDF-Daten im OCI Object Storage zugreifen kann (mit dem Package DBMS\_CLOUD), müssen Sie ein Zugriffstoken mit Ihrem OCI-Account erstellen. Dies wird in der sekundären Übung verwendet.

Geschätzte Zeit: 5 Minuten

### Ziele

*   RDF-Daten in OCI Object Storage hochladen
*   OCI-Benutzernamen anzeigen
*   Zugriffstoken generieren

### Voraussetzungen

In dieser Übung wird Folgendes vorausgesetzt:

*   Oracle Cloud-Account
*   Laden Sie die MOVIESTREAM-Datei (moviestream\_rdf.nt) mit diesem [Link](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt) herunter

## **Aufgabe 1:** RDF-Daten in OCI Object Storage hochladen

1.  Melden Sie sich mit Ihren Oracle Cloud-Zugangsdaten bei der OCI-Konsole an.
2.  Öffnen Sie das Navigationsmenü, und klicken Sie auf "Speicher". Klicken Sie unter Object Storage und Archive Storage auf Buckets wie dargestellt: ![Bild, das beschreibt, wo der Bucket-Ordner im Menü ausgewählt ist](./images/buckets-folder.png)
3.  Wählen Sie ein Compartment aus, das für Ihren OCI-Account gilt. ![Bild, das zeigt, wo sich das Dropdown-Menü "Compartment" auf der Seite "Buckets" befindet](./images/compartment-menu.png)
4.  Klicken Sie auf {\\b Create Bucket}. Der Schieberegler "Create Bucket" wird geöffnet (siehe Abbildung): ![Bild mit einer Beschreibung der Seite "Bucket erstellen"](./images/create-bucket.png)
5.  Geben Sie den Bucket-Namen ein, übernehmen Sie alle anderen Elemente als Standard, und klicken Sie auf "Erstellen". Der Bucket wird erstellt und auf der Seite "Buckets" wie dargestellt aufgelistet: ![Bild mit dem Ergebnis der Erstellung eines Buckets](./images/bucket-result.png)
6.  Klicken Sie auf den Link RDF\_DATA\_BUCKET, und navigieren Sie zur Seite "Bucket-Details".

![Bild, das die Seite "Bucket" nach der Erstellung anzeigt](./images/bucket-page.png) 7. Klicken Sie im Abschnitt Objekte auf Hochladen. Der Schieberegler "Objekte hochladen" wird geöffnet. 8. Wählen Sie den heruntergeladenen [Link](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt) der RDF-Datei moviestream\_rdf.nt in Ihrem lokalen System aus, und klicken Sie auf "Hochladen". Die Datei wurde erfolgreich hochgeladen. Klicken Sie auf "Schließen", um zur Seite "Bucket-Details" zurückzukehren. Die hochgeladene Datei wird wie dargestellt unter "Objects" aufgeführt: ![Bild mit dem Objekt, das in den Bucket hochgeladen wurde](./images/image-upload.png)

1.  Wählen Sie das Menü "Aktionen" für die hochgeladene Datei, und klicken Sie auf "Objektdetails anzeigen", um auf die Eigenschaften der hochgeladenen Datei zuzugreifen. Der Schieberegler "Object Details" wird wie dargestellt geöffnet: ![Bild mit dem angezeigten Objektmenü, das die Option "Objektdetails anzeigen" hervorhebt](./images/object-details.png)
2.  Notieren Sie den URL-Pfad des Objekts. Wird im RDF-Importassistenten in Graph Studio verwendet. ![Bild, das zeigt, wo der URL-Pfad zum Objekt im Bucket gefunden wird](./images/url-path.png)

## **Aufgabe 2:** Ihren OCI-Benutzernamen anzeigen

1.  Klicken Sie auf das Avatarsymbol in der oberen rechten Ecke, um Ihr Profil zu öffnen. Der erste Eintrag unter "Profil" ist Ihr OCI-Benutzername. ![Bild mit dem Zugriff auf das OCI-Profil](./images/oci-profile.png)
2.  Notieren Sie sich Ihren OCI-Benutzernamen. Wird im RDF-Importassistenten in Graph Studio verwendet. ![Bild mit dem OCI-Benutzernamen aus den Benutzerdetails](./images/oci-username.png)

## **Aufgabe 3:** Zugriffstoken über die OCI-Konsole generieren

1.  Melden Sie sich mit Ihren Oracle Cloud-Zugangsdaten bei der OCI-Konsole an.
    
2.  Klicken Sie auf das Avatarsymbol in der oberen rechten Ecke, um Ihr Profil zu öffnen, und klicken Sie auf "Benutzereinstellungen". ![Bild mit dem Zugriff auf Benutzereinstellungen über das Profil](./images/user-settings.png)
    
3.  Klicken Sie wie dargestellt unter Ressourcen auf Authentifizierungstoken: ![Bild, das den Zugriff auf Authentifizierungstoken über das Menü "Ressourcen" in den Benutzereinstellungen zeigt](./images/auth-tokens.png)
    
4.  Klicken Sie auf {\\b Generate Token}. Das Dialogfeld "Token generieren" wird geöffnet. ![Bild, das zeigt, wie ein Authentifizierungstoken generiert wird](./images/gen-tokens.png)
    
5.  Geben Sie eine Beschreibung ein, und klicken Sie auf "Generate Token". Die Details des generierten Tokens werden wie folgt angezeigt: ![Bild, das zeigt, wie das generierte Authentifizierungstoken kopiert wird](./images/token-details.png)
    
6.  Klicken Sie auf "Kopieren", um das Token zu kopieren und es zur späteren Verwendung zu speichern.
    

Damit endet diese Übung. _Jetzt können Sie mit der nächsten Übung fortfahren._

## Danksagungen

*   **Autor** - Melliyal Annamalai, Distinguished Product Manager
*   **Technischer Mitwirkender** - Nicholas Cusato, Santa Monica Specialist Hub
*   **Zuletzt aktualisiert am/um** - Nicholas Cusato, Santa Monica Specialist Hub, 25. Februar 2022