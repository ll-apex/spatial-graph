# Verbindung zu Autonomous Database über Python herstellen

## Einführung

Um sich auf das Laden und Analysieren von Daten vorzubereiten, stellen Sie zunächst eine Verbindung von Python zu Autonomous Database her. Der python-oracledb-Treiber unterstützt diese Verbindung und alle nachfolgenden Datenbankinteraktionen. Sie verwenden den "Thin"-Modus des python-oracledb-Treibers, der direkt mit Oracle Database verbunden wird und keine Oracle-Client-Librarys benötigt.

Geschätzte Laborzeit: 5 Minuten

### Ziele

*   Verbindung zu Autonomous Database über Python herstellen

### Voraussetzungen

*   Abschluss von Übung 3: Starten Sie JupyterLab

## Aufgabe 1: Verbindungsparameterdateien erstellen

1.  Um zu vermeiden, dass Datenbankverbindungsinformationen direkt in Ihr Notizbuch aufgenommen werden, erstellen Sie Dateien mit diesen Informationen, auf die Ihr Notizbuch verweisen kann. Klicken Sie in JupyterLab auf die Kachel "Textdatei", um eine neue Textdatei zu erstellen. ![Mit ADB verbinden](images/connect-to-adb-01.png)
    
2.  Geben Sie Ihr ADB-ADMIN-Benutzerkennwort ein. Wählen Sie dann im Menü "Datei" die Option **Text speichern**. ![Mit ADB verbinden](images/connect-to-adb-02.png)
    
3.  Wenn Sie dazu aufgefordert werden, geben Sie **my-pwd.txt** als Dateinamen ein, und klicken Sie auf **Umbenennen**. ![Mit ADB verbinden](images/connect-to-adb-03.png)
    
4.  Schließen Sie die Registerkarte "Textdatei", um zur Seite "Launcher" zurückzukehren. ![Mit ADB verbinden](images/connect-to-adb-04.png)
    
5.  Kehren Sie zur Oracle Cloud-Browserregisterkarte zurück, und minimieren Sie Cloud Shell. ![Mit ADB verbinden](images/connect-to-adb-05.png)
    
6.  Klicken Sie auf **Datenbankverbindung**. ![Mit ADB verbinden](images/connect-to-adb-06.png)
    
7.  Blättern Sie nach unten zum Abschnitt Verbindungszeichenfolgen. Wählen Sie für die TLS-Authentifizierung die Option **TLS** aus. Dies ist erforderlich, um Verbindungen im Thin-Modus zuzulassen. Klicken Sie dann unter Verbindungszeichenfolge auf **Kopieren**, um den TNS-Namen mit der Endung \_low anzuzeigen. ![Mit ADB verbinden](images/connect-to-adb-07.png)
    
8.  Kehren Sie zur Browserregisterkarte JupyterLab zurück. Klicken Sie wie zuvor auf die Kachel "Textdatei", um eine neue Textdatei zu erstellen. Fügen Sie die soeben aus Autonomous Database kopierte Verbindungszeichenfolge ein. Speichern Sie die Datei, und benennen Sie sie in **my-dsn.txt** um. ![Mit ADB verbinden](images/connect-to-adb-08.png)
    

Schließen Sie wie zuvor die Registerkarte "Textdatei", um zur Seite "Launcher" zurückzukehren.

## Aufgabe 2: Notizbuch erstellen und Verbindung zu Autonomous Database herstellen

1.  Klicken Sie im Launcher auf die Kachel **Python 3**, um ein neues Notizbuch zu erstellen. ![Mit ADB verbinden](images/connect-to-adb-09.png)
    
2.  Fügen Sie in der ersten Zelle die folgende Anweisung ein, und klicken Sie auf die Schaltfläche **Ausführen**. Dadurch wird das python-oracedb-Modul geladen, das die Interaktion mit Oracle Database verarbeitet.
    
        <copy>
        import oracledb
        </copy>
        
    
    ![Mit ADB verbinden](images/connect-to-adb-10.png)
    
3.  Fügen Sie in der nächsten Zelle die folgenden Anweisungen ein, und klicken Sie auf die Schaltfläche **Ausführen**. Dadurch wird das ADB-Kennwort und der DSN in Variablen geladen
    
        <copy>
        # Get ADB password and DSN from file
        my_pwd = open('./my-pwd.txt','r').readline().strip()
        my_dsn = open('./my-dsn.txt','r').readline().strip()
        </copy>
        
    
    ![Mit ADB verbinden](images/connect-to-adb-11.png)
    
4.  Fügen Sie in der nächsten Zelle die folgenden Anweisungen ein, und klicken Sie auf die Schaltfläche **Ausführen**. Dadurch wird eine Verbindung zu Ihrer ADB hergestellt.
    
        <copy>
        # Create database connection and cursor
        connection = oracledb.connect(user="admin", password=my_pwd, dsn=my_dsn)
        cursor = connection.cursor()
        </copy>
        
    
    ![Mit ADB verbinden](images/connect-to-adb-12.png)
    
5.  Fügen Sie in der nächsten Zelle die folgenden Anweisungen ein, und klicken Sie auf die Schaltfläche **Ausführen**. Dadurch wird eine Testabfrage ausgeführt, um eine erfolgreiche Verbindung zu ADB zu prüfen.
    
        <copy>
        # Run a test query
        cursor.execute("select object_type, count(*) from all_objects group by object_type")
        for row in cursor.fetchmany(size=10):
          print(row)
        </copy>
        
    
    ![Mit ADB verbinden](images/connect-to-adb-13.png)
    
6.  Klicken Sie im linken Bereich mit der rechten Maustaste auf die Notizbuchdatei Untitled.ipynb, und wählen Sie **Umbenennen** aus.
    
    ![Mit ADB verbinden](images/connect-to-adb-14.png)
    
7.  Geben Sie **my-notebook** (oder einen Namen Ihrer Wahl) ein. Beachten Sie, dass der Notizbuchname geändert wurde.
    
    ![Mit ADB verbinden](images/connect-to-adb-15.png)
    

Sie können jetzt **mit der nächsten Übung fortfahren**.

## Weitere Informationen

*   Weitere Informationen zu python-oracledb-Verbindungen zu Autonomous Database finden Sie in der [Dokumentation](https://python-oracledb.readthedocs.io/en/latest/user_guide/connection_handling.html#connecting-to-oracle-cloud-autonomous-databases).

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Mitwirkende** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Zuletzt aktualisiert am/um** - David Lapp, August 2023