# Diagramm visualisieren

## Einführung

Die Ergebnisse der in den vorherigen Übungen durchgeführten Analysen können mit der Graphvisualisierungsfunktion einfach visualisiert werden.

Voraussichtliche Zeit: 5 Minuten

Das folgende Video bietet einen Überblick über die Komponente "Diagrammvisualisierung" (= GraphViz).

[YouTube](youtube:zfefKdNfAY4)

### Ziele

*   Erfahren Sie, wie Sie PGQL-Diagrammabfragen ausführen und die Ergebnisse visualisieren.

### Voraussetzungen

*   Der Graph wird erstellt und veröffentlicht
*   Der Graph Server (mit GraphViz) ist hochgefahren und wird ausgeführt

## Aufgabe 1: Melden Sie sich bei GraphViz an

Öffnen Sie GraphViz unter **`https://<public_ip_for_compute>:7007/ui`** mit einem Webbrowser. Ersetzen Sie **`<public_ip_for_compute>`** durch die für die Graph Server-Compute-Instanz.

Da das Marketplace-Image mit einem selbstsignierten SSL-Zertifikat verteilt wird, sollten Sie es für Ihr eigenes Zertifikat in der Produktionsumgebung ändern. Inzwischen sollten Webbrowser Warnungen anzeigen, während wir verstehen, dass es sicher ist.

Wenn Sie **Chrome** verwenden, geben Sie **thisisunsafe** in das Warnfenster ein, um zum Bildschirm GraphViz zu gelangen.

![Login-Chrome](images/login-chrome.jpg)

Klicken Sie in **Firefox** auf **Erweitert** und dann auf **Risiko akzeptieren und fortfahren**.

![Login-firefox](images/login-firefox.jpg)

Sie sollten einen Bildschirm wie den Screenshot unten sehen. Geben Sie den Benutzernamen (**customer\_360**) und das Kennwort ein, und klicken Sie auf "Submit". **Grafikserver** ist der Standardwert in den erweiterten Optionen. Sie müssen ihn also nicht ändern.

![Anmelden](images/login.jpg)

## Aufgabe 2: Abfrage ändern

Ändern Sie die Abfrage so, dass die ersten 5 Zeilen abgerufen werden. Ändern Sie also **LIMIT 100** in **LIMIT 5**, und klicken Sie auf "Ausführen".

Sie sollten ein Diagramm wie im folgenden Screenshot sehen.

![show-5-Elemente](images/show-5-elements.jpg)

## Aufgabe 3: Highlights hinzufügen

Lassen Sie uns nun einige Labels und anderen visuellen Kontext hinzufügen. Diese werden als Highlights bezeichnet. Klicken Sie [hier](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/highlights.json.zip), um eine ZIP-Datei herunterzuladen, highlights.json.zip. Dekomprimieren Sie diese Datei, und notieren Sie sich, wo sie dekomprimiert wurde.

Klicken Sie unter **Einstellungen** (rechts auf dem Bildschirm) auf die Schaltfläche "Load". Navigieren Sie zum entsprechenden Ordner, wählen Sie die Datei aus, und klicken Sie auf "Öffnen", um die Datei zu laden.

![Highlights-1](images/highlights-1.png)

Das Diagramm sollte nun wie

![Highlights-2](images/highlights-2.png)

## Aufgabe 4: Musterabgleich mit PGQL

1.  Als Nächstes führen wir einige PGQL-Abfragen aus.
    
    Die Site [pgql-lang.org](http://pgql-lang.org) und die [Spezifikation](http://pgql-lang.org/spec/1.4) sind die besten Referenzen für Details und Beispiele. Für die Zwecke dieser Übung sind hier jedoch minimale Grundlagen.
    
    Die allgemeine Struktur einer PGQL-Abfrage lautet:
    
        <copy>
        SELECT <select_list>
        FROM MATCH <graph_pattern> ON <graph_name>
        WHERE <condition>
        </copy>
        
    
    PGQL stellt ein bestimmtes Konstrukt bereit, das als **MATCH**\-Klausel für den Abgleich von Diagrammmustern bezeichnet wird. Ein Diagrammmuster entspricht Scheiteln und Kanten, die den angegebenen Bedingungen und Einschränkungen entsprechen.
    
    *   **(v)** gibt eine Scheitelvariable **v an**
    *   **\-** gibt eine ungerichtete Kante an, wie in (Quelle)-(Ziel)
    *   **\->** eine ausgehende Edge von Quelle zu Ziel
    *   **<-** eine eingehende Edge von Ziel zu Quelle
    *   **\[e\]** gibt eine Kantenvariable **e an**
    
    Lassen Sie außerdem die **graph\_name** hier weg, da sie in der Benutzeroberfläche von GraphViz ausgewählt ist.
    
2.  Lassen Sie uns Konten finden, die am selben Tag eine ausgehende und eingehende Übertragung von über 500 hatten.
    
    Die PGQL-Abfrage hierfür lautet:
    
        <copy>
        SELECT *
        FROM MATCH (a)-[t1:transfer]->(a1)
           , MATCH (a2)-[t2:transfer]->(a)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
        </copy>
        
    
    In der ersten **MATCH**\-Klausel oben gibt **(a)** den Quellscheitel und **(a1)** das Ziel an, während **\[t1:transfer\]** die Edge ist, die sie verbindet. **:transfer** gibt an, dass die **t1**\-Edge das Label **TRANSFER** aufweist. Das Komma (,) zwischen den beiden Mustern ist eine UND-Bedingung.
    
3.  Kopieren Sie die Abfrage, und fügen Sie sie in das Texteingabefeld "PGQL-Diagrammabfrage" der Anwendung GraphViz ein. Klicken Sie auf "Run".
    
    Das Ergebnis sollte wie unten dargestellt aussehen. In den Hervorhebungseinstellungen werden die Konten, die mit **xxx-yyy-** beginnen, rot angezeigt (= Konten der Bank), während **xxx-zzz-** orangefarben dargestellt wird (= Konten einer anderen Bank).
    
    ![Transfers am selben Tag](images/same-day-transfers.jpg)
    
4.  Die nächste Abfrage findet Muster von Übertragungen von und zu denselben beiden Konten, d.h. von a1->a2 und zurück a2->a1.
    
    Die PGQL-Abfrage hierfür lautet:
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
        </copy>
        
5.  Kopieren Sie die Abfrage, und fügen Sie sie in das Texteingabefeld "PGQL-Diagrammabfrage" der Anwendung GraphViz ein. Klicken Sie auf "Run".
    
    Das Ergebnis sollte wie unten dargestellt aussehen.
    
    ![Zyklus-2-Hops](images/cycle-2-hops.jpg)
    
6.  Fügen wir dieser Abfrage ein weiteres Konto hinzu, um ein zirkuläres Transfermuster zwischen 3 Konten zu finden.
    
    Die PGQL-Abfrage wird zu:
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
        </copy>
        
7.  Kopieren Sie die Abfrage, und fügen Sie sie in das Texteingabefeld "PGQL-Diagrammabfrage" der Anwendung GraphViz ein. Klicken Sie auf "Run".
    
    Das Ergebnis sollte wie unten dargestellt aussehen.
    
    ![Zyklus-3-Hops](images/cycle-3-hops.jpg)
    

## Danksagungen

*   **Autor** - Jayant Sharma
*   **Mitwirkende** - Arabella Yao, Jenny Tsai
*   **Zuletzt aktualisiert am/um** - Ryota Yamanaka, März 2023