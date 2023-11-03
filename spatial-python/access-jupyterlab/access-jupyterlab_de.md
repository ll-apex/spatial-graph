# Auf JupyterLab zugreifen

## Einführung

Notizbücher sind interaktive Dokumente für Code, beschreibenden Text und Visualisierungen. In diesem Workshop verwenden Sie Open Source JupyterLab, das eine webbasierte Notizbuchumgebung mit vielen benutzerfreundlichen Funktionen wie Dateiupload bereitstellt.

Geschätzte Laborzeit: 5 Minuten

### Ziele

*   Zugriff auf JupyterLab prüfen
*   Notizbuchfunktionalität untersuchen
*   Option auswählen, um die verbleibende praktische Übung durchzuführen

## Aufgabe 1: IP-Adresse für JupyterLab abrufen

1.  Navigieren Sie vom Hauptmenü zu Compute > Instances

![IP-Adresse abrufen](images/compute-01.png)

2.  Klicken Sie auf der Seite mit den Workshop-Anweisungen oben links auf **Anmeldeinformationen anzeigen**, und kopieren Sie Ihren Compartment-Namen.

![IP-Adresse abrufen](images/compartment.png)

1.  Fügen Sie in der OCI-Konsole Ihren Compartment-Namen ein, und wählen Sie ihn im Pulldown-Menü aus.

![IP-Adresse abrufen](images/compute-02.png)

4.  Notieren Sie sich die öffentliche IP der Compute-Instanz. JupyerLab wurde auf dieser Instanz festgelegt. Sie werden dies später in dieser und anderen Übungen verwenden.

![IP-Adresse abrufen](images/compute-03.png)

## Aufgabe 2: Zugriff auf JupyterLab prüfen

1.  Öffnen Sie eine neue Browserregisterkarte, und geben Sie die URL **http://\[IP-Adresse\]:8001/lab** ein. Dabei ist \[IP-Adresse\] die in Aufgabe 1 abgerufene Adresse.
    
    ![Auf JupyterLab zugreifen](images/access-jupyter-01.png)
    
2.  Geben Sie das Kennwort **livelabs** ein, und klicken Sie auf **Anmelden**.
    

## Aufgabe 2: Jupyter-Notizbücher durchsuchen

Jupyter Notebook ist ein interaktives webbasiertes Tool, mit dem Sie Dokumente erstellen und freigeben können, die Livecode, Gleichungen, Visualisierungen und Text enthalten. Es wird häufig in der Data Science-Community für Prototyping und Datenanalyse verwendet.

In dieser Aufgabe werden die Grundlagen der Verwendung von Jupyter Notebook erläutert.

1.  Erstellen Sie ein neues Notizbuch.
    
    Wenn die Jupyter-Umgebung geladen wird, sollte eine Startertabelle geöffnet sein.
    
    ![Starter-Registerkarte ist geöffnet](./images/launcher1.png)
    
    Wenn das Starterfenster nicht angezeigt wird, wählen Sie oben links im Fenster "Datei" und dann "Neuer Starter".
    
    ![Neue Launcher-Registerkarte öffnen](./images/launcher2.png)
    
    Wählen Sie im Starterfenster "Python 3", um ein neues Notizbuch mit der Python-Programmiersprache zu erstellen. Ein neues Notizbuch wird erstellt. Sie können damit beginnen, indem Sie Code in die Codezellen eingeben oder Markdown-Text in die Markdown-Zellen hinzufügen.
    
    ![Neues Python-Notizbuch erstellen](./images/launcher3.png)
    
2.  Fügen Sie einen Markdown-Text hinzu.
    
    Klicken Sie auf die Codezelle und verwenden Sie die Dropdown-Liste "Zelltyp", um "Markdown" auszuwählen
    
    ![Markdown-Zelle hinzufügen](./images/notebook1.png)
    
    Fügen Sie Folgendes in die Zelle ein, und klicken Sie auf die Wiedergabeschaltfläche in der Symbolleiste, oder drücken Sie Shift+Enter, um die Zelle auszuführen.
    
        	<copy>
        	# My First Notebook
        	This is my first Jupyter notebook
        	</copy>
        
    
    ![Ergebnis der Preisabschrift](./images/notebook2.png)
    
3.  Schreiben Sie einen Python-Code. Fügen Sie Folgendes in die nächste Zelle ein, und führen Sie es aus. Der Satz "Hallo, Welt!" sollte unter der Zelle erscheinen.
    
        	<copy>
        	print('Hello, World!')
        	</copy>
        
        
    
    ![Hallo Welt Beispiel](./images/notebook3.png)
    
4.  Um ein Jupyter Notebook zu speichern, klicken Sie in der Symbolleiste auf das Symbol "Speichern", oder drücken Sie Ctrl+S (oder Cmd+S auf macOS). Das Notizbuch wird mit der Dateierweiterung .ipynb gespeichert.
    

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Mitwirkende** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Zuletzt aktualisiert am/um** - David Lapp, August 2023