# Diagramm aus vorhandenen relationalen Daten mit Graph Studio erstellen

## Einführung

In dieser Übung lernen Sie mehr über Graph Studio und erfahren, wie Sie Diagramme aus vorhandenen relationalen Daten erstellen können, die in Ihrer Autonomous Data Warehouse - Shared Infrastructure-(ADW-) oder Autonomous Transaction Processing - Shared Infrastructure-(ATP-)Instanz gespeichert sind.

Geschätzte Zeit: 30 Minuten.

### Ziele

*   Erfahren Sie, wie Sie ein Diagramm aus dem Beispiel-Dataset "Vertriebshistorie" (SH) modellieren
*   Erfahren Sie, wie Sie einen Diagrammerstellungsjob überwachen
*   Erfahren Sie, wie Sie erstellte Diagramme und Diagrammmodelle prüfen

### Voraussetzungen

*   Für die folgende Übung ist ein Account für Autonomous Data Warehouse - Shared Infrastructure oder Autonomous Transaction Processing - Shared Infrastructure erforderlich.
*   Es wird davon ausgegangen, dass Sie die erste Übung abgeschlossen haben, in der erläutert wird, wie Sie auf die Graph Studio-Oberfläche Ihrer Datenbankinstanz zugreifen können. Außerdem werden einige grundlegende Konzepte erläutert.

## Aufgabe 1: Erforderliche Ansichten erstellen

1.  Wählen Sie auf der Seite "Autonomous Database-Details" in OCI die Option "Datenbankaktionen" aus
    
    ![Wählen Sie auf der Seite "Autonome Datenbank - Details" die Option "Database Actions" aus](./images/select-database-actions.png "Wählen Sie auf der Seite "Autonome Datenbank - Details" die Option "Database Actions" aus")
    
2.  Standardmäßig werden Sie als Admin-Benutzer angemeldet. Melden Sie sich ab und wieder als Graph-Benutzer an.
    

![Bei Database Actions abmelden](./images/sign-out-database-actions.png "Bei Database Actions abmelden") ![Melden Sie sich als Graphbenutzer bei Database Actions an](./images/sign-in-db-actions.png "Melden Sie sich als Graphbenutzer bei Database Actions an")

3.  SQL auswählen

![SQL aus Database Actions auswählen](./images/select-sql-db-actions.png "SQL aus Database Actions auswählen")

4.  In dieser Übung verwenden wir das Beispielschema {\\b Sales History} (SH), um unser Demodiagramm zu erstellen. Das SH-Schema ist in allen Autonomous Database-Instanzen verfügbar. Erstellen Sie Ansichten für CUSTOMERS, TIMES, CHANNELS, PRODUCTS und PROMOTIONS aus den SH-Tabellen, wobei Sie nur eine Teilmenge der Spalten aus diesen Tabellen verwenden.

    <copy>
    CREATE OR REPLACE VIEW SH_CUSTOMERS_VIEW (CUST_ID, CUST_FIRST_NAME, CUST_LAST_NAME, CUST_EMAIL, CUST_GENDER, CUST_CITY, CUST_STATE_PROVINCE, COUNTRY_ID)
    	DEFAULT COLLATION "USING_NLS_COMP"  AS
    	select cust_id, cust_first_name, cust_last_name, cust_email, cust_gender, cust_city, cust_state_province, country_id from sh.customers;
    
    CREATE OR REPLACE  VIEW SH_CHANNELS_VIEW (CHANNEL_ID, CHANNEL_DESC, CHANNEL_CLASS) DEFAULT COLLATION "USING_NLS_COMP"  AS
    	select channel_id, channel_desc, channel_class from sh.channels ;
    
    CREATE OR REPLACE VIEW SH_TIMES_VIEW (ID, TIME_ID, DAY_NAME, DAY_NUMBER_IN_MONTH, CALENDAR_MONTH_NUMBER,  CALENDAR_YEAR)
    	DEFAULT COLLATION "USING_NLS_COMP"  AS select rownum id, time_id, day_name, day_number_in_month, calendar_month_number, calendar_year from sh.times ;
    
    CREATE OR REPLACE VIEW SH_PRODUCTS_VIEW (PROD_ID, PROD_NAME, PROD_DESC, PROD_CATEGORY, PROD_STATUS)
    	DEFAULT COLLATION "USING_NLS_COMP"  AS select cast(prod_id as number) as prod_id, prod_name, prod_desc, prod_category, prod_status from sh.products;
    
    CREATE OR REPLACE VIEW SH_PROMOTIONS_VIEW (PROMO_ID, PROMO_NAME, PROMO_SUBCATEGORY, PROMO_CATEGORY, PROMO_COST)
    	DEFAULT COLLATION "USING_NLS_COMP"  AS select cast(promo_id as number) promo_id, promo_name, promo_subcategory, promo_category, promo_cost from sh.promotions;
    
    CREATE OR REPLACE VIEW SH_SALES_VIEW (SALE_ID, CUST_ID, PROD_ID, PROMO_ID, DATE_OF_SALE_ID, CHANNEL_ID, AMOUNT_SOLD, QUANTITY_SOLD)
    	DEFAULT COLLATION "USING_NLS_COMP" AS
    	select rownum sale_id, s.cust_id, s.prod_id, s.promo_id, tv.id as date_of_sale_id, s.channel_id, s.amount_sold, s.quantity_sold from sh.sales s, sh_times_view tv where s.time_id = tv.time_id
    </copy>
    

![Führen Sie den kopierten Code aus, um Ansichten für KUNDEN, TIMES, KANäle, Produkte und Angebote zu erstellen](./images/create-views.png "Ansichten für KUNDEN, ZEITEN, KANALEN, PRODUKTE und PROMOTIONEN erstellen")

5.  Relevante Primärschlüssel zu den Ansichten hinzufügen

    <copy>
    ALTER VIEW SH_CUSTOMERS_VIEW ADD CONSTRAINT SH_CUSTOMER_VIEW_PK PRIMARY KEY (CUST_ID) DISABLE ;
    
    ALTER VIEW SH_CHANNELS_VIEW ADD CONSTRAINT SH_CHANNEL_VIEW_PK PRIMARY KEY (CHANNEL_ID) DISABLE ;
    
    ALTER VIEW SH_TIMES_VIEW ADD CONSTRAINT SH_TIMES_VIEW_PK PRIMARY KEY (ID) DISABLE ;
    
    ALTER VIEW SH_PRODUCTS_VIEW ADD CONSTRAINT SH_PRODUCT_VIEW_PK PRIMARY KEY (PROD_ID) DISABLE;
    
    ALTER VIEW SH_PROMOTIONS_VIEW ADD CONSTRAINT SH_PROMO_VIEW_PK PRIMARY KEY (PROMO_ID) DISABLE;
    
    ALTER VIEW SH_SALES_VIEW ADD CONSTRAINT SH_SALES_VIEW_PK PRIMARY KEY (SALE_ID) DISABLE;
    </copy>
    

![Relevante Primärschlüssel zu den Ansichten hinzufügen](./images/add-view-pks.png "Relevante Primärschlüssel zu den Ansichten hinzufügen")

6.  Relevante Fremdschlüssel für die Vertriebsansicht hinzufügen

    <copy>
    ALTER VIEW SH_SALES_VIEW ADD CONSTRAINT SH_SALES_PROMO_VIEW_FK FOREIGN KEY (PROMO_ID) REFERENCES SH_PROMOTIONS_VIEW (PROMO_ID) DISABLE;
    
    ALTER VIEW SH_SALES_VIEW ADD CONSTRAINT SH_SALES_PRODUCT_VIEW_FK FOREIGN KEY (PROD_ID) REFERENCES SH_PRODUCTS_VIEW (PROD_ID) DISABLE;
    
    ALTER VIEW SH_SALES_VIEW ADD CONSTRAINT SH_SALES_CUST_VIEW_FK FOREIGN KEY (CUST_ID) REFERENCES SH_CUSTOMERS_VIEW (CUST_ID) DISABLE ;
    
    ALTER VIEW SH_SALES_VIEW ADD CONSTRAINT SH_SALES_CHANNEL_VIEW_FK FOREIGN KEY (CHANNEL_ID) REFERENCES SH_CHANNELS_VIEW (CHANNEL_ID) DISABLE ;
    
    ALTER VIEW SH_SALES_VIEW ADD CONSTRAINT SH_SALES_TIMES_VIEW_FK FOREIGN KEY (DATE_OF_SALE_ID) REFERENCES SH_TIMES_VIEW (ID) DISABLE ;
    </copy>
    

![Fügen Sie die relevanten Fremdschlüssel für SH_SALES_VIEW hinzu.](./images/add-view-fks.png "Fügen Sie die relevanten Fremdschlüssel für SH_SALES_VIEW hinzu.")

7.  Nachdem Sie die erforderlichen Ansichten erstellt haben, können Sie ein Diagramm in Graph Studio erstellen. Navigieren Sie also zurück zur Seite "Autonomous Database-Details" in OCI, wählen Sie "Tools" und dann "Open Graph Studio" aus.

![Graph Studio öffnen](./images/open-graph-studio.png "Graph Studio öffnen")

8.  Melden Sie sich mit Ihrem Graph-Benutzer bei Graph Studio an

![Melden Sie sich mit Ihrem Graph-Benutzer bei Graph Studio an](./images/graph-studio-login.png "Melden Sie sich mit Ihrem Graph-Benutzer bei Graph Studio an")

## Aufgabe 2: Wählen Sie die Tabellen, aus denen das Diagramm erstellt werden soll

1.  Der folgende Screenshot zeigt die Graph Studio-Benutzeroberfläche mit den Symbolen für das Menü oder die Navigation auf der linken Seite. Sie navigieren zu den Seiten "Home", "Modelle", "Diagramme", "Notizbücher" und "Jobs".
    
    ![Homepage mit Inhalt](./images/home-page-with-content.png "Seite "Diagramme" ")
    
2.  Klicken Sie auf das Menüsymbol **Diagramme** und dann auf "Erstellen".
    
    ![Seite "Diagramme"](./images/graph-page.png " ")
    
    In dieser Übung verwenden wir die Ansichten, die aus dem Beispielschema {\\b Sales History} (SH) erstellt wurden, um unser Demodiagramm zu erstellen. Das SH-Schema ist in allen Autonomous Database-Instanzen verfügbar. Sie können die Schritte dieser Übung jedoch auf alle relationalen Daten anwenden, die in Ihrer Datenbank verfügbar sind, unabhängig davon, woher die Daten stammen. Alle Schemas und Tabellen, auf die Sie Zugriff haben, werden zu Beginn des Modellierungsworkflows als mögliche Eingabetabellen angezeigt.
    
3.  Öffnen Sie das Schema **GRAPHUSER**, und doppelklicken Sie auf die Tabelle **SH\_PRODUCTS\_VIEW**.
    
    Sie sehen einige Details zu dieser Tabelle, wie alle Spalten und deren Typen, sowie die Spalte, die der Primärschlüssel ist:
    
    ![Modeler-Ansicht von SH_PRODUCTS_VIEW](./images/modeler-view-products-view-info.png "Modeler-Ansicht von SH_PRODUCTS_VIEW ")
    
4.  Klicken Sie unten links auf die Registerkarte **GRAPHUSER.SH\_PRODUCTS\_VIEW - Data**.
    
    Eine Vorschau der Werte dieser Tabelle wird angezeigt. Standardmäßig werden die ersten zehn Zeilen angezeigt. Sie können jedoch die Stichprobengröße erhöhen. Sie können auch nach einem beliebigen Wert in dieser Tabelle suchen und durch die Vorschau paginieren.
    
5.  In dieser Übung wählen wir alle zuvor erstellten Ansichten als Eingabe für unser Diagrammmodell aus. Wenn Ihr Graphbenutzer nur diese Ansichten enthält, können Sie _GRAPHUSER_ auswählen und dann auf die Schaltfläche in der Mitte klicken, um alle Ansichten in den ausgewählten Abschnitt auf der rechten Seite zu verschieben. Wählen Sie andernfalls die entsprechenden Ansichten aus, und klicken Sie dann auf die Schaltfläche in der Mitte, um alle Ansichten in den ausgewählten Abschnitt auf der rechten Seite zu verschieben.
    
    ![Wählen Sie alle relevanten Ansichten für das Diagramm aus](./images/modeler-views-selected.png "Wählen Sie alle relevanten Ansichten für das Diagramm aus ")
    
6.  Klicken Sie oben rechts auf die Schaltfläche **Weiter**, um zum nächsten Schritt zu gelangen. Graph Studio analysiert die Fremdschlüssel-Constraints und schlägt eine mögliche Zuordnung von den ausgewählten Ansichten zu einer Eigenschaftsdiagrammstruktur vor. Dies kann einige Sekunden dauern. Wenn Sie fertig sind, sehen Sie alle Eingaben auf der linken Seite und die Zuordnung zu Scheitel- und Kanten-Tabellen auf der rechten Seite.
    
    ![Modeler-Ausgabe des Diagrammmodells aus eingegebenen Ansichten](./images/modeler-sh-model.png "Modeler-Ausgabe des Diagrammmodells aus eingegebenen Ansichten ")
    
    Dieses Modell kann bei Bedarf geändert werden.
    

## Aufgabe 3: Diagrammmodell bearbeiten

1.  Klicken Sie auf die Scheiteltabelle **SH\_CHANNELS\_VIEW**.
    
    Der automatische Diagrammmodellierer empfiehlt, jede Zeile der _SH\_CHANNELS\_VIEW_\-Eingabe in einen Scheitel im Zieleigenschaftsdiagramm zu konvertieren. Im Eigenschaftsdiagrammmodell können Scheitel und Kanten ein _Label_ aufweisen, um sie in verschiedene Arten von Scheiteln und Kanten zu kategorisieren. Jedem Label können unterschiedliche Eigenschaften zugeordnet sein. Der Graph Modeler setzt das Label automatisch auf den Namen der Eingabetabelle. Auf diese Weise können wir später leicht erkennen, von welchem Typ jeder Scheitel oder jede Kante in unserem generierten Diagramm ist. Außerdem wird angezeigt, dass jede _Spalte_ der Eingabetabelle in eine _Eigenschaft_ in unserem Diagrammmodell konvertiert wurde. Im Eigenschaftsdiagrammmodell sind Eigenschaften beliebige Schlüssel/Wert-Paare, die jedem Scheitel oder jeder Kante in unserem Diagramm zugeordnet sind. Durch die Zuordnung aller Spaltenwerte zu Eigenschaften wird sichergestellt, dass alle Eingabedaten in unserem Diagramm beibehalten werden.
    
    Mit dem Graph Modeler können Sie jedoch die Zuordnung von Daten anpassen und unnötige Tabellen und/oder Spalten entfernen, die für Ihre Analyse nicht relevant sind. Durch die Reduzierung der zu verarbeitenden Datenmenge werden die für die Diagrammanalyse erforderlichen Verarbeitungsressourcen und Speicher reduziert. Beim Erstellen der Ansichten für dieses Diagramm wurden unnötige Spalten entfernt. Daher ist in dieser Instanz nichts zu entfernen.
    
2.  Benennen Sie das Scheitellabel in **CHANNELS** um:
    
    ![CHANNELS Vertex Label umbenennen](./images/model-rename-vertex.png "CHANNELS Vertex Label umbenennen ")
    
3.  Wiederholen Sie den Vorgang für alle anderen Scheiteltabellen:
    
    | Name der aktuellen Ansicht | Umbenanntes Knotenlabel |
    | --- | --- |
    | SH\_SALES\_VIEW | VERKAUF |
    | SH\_CUSTOMERS\_VIEW | KUNDEN |
    | SH\_TIMES\_VIEW | ZEITEN |
    | SH\_PROMOTIONS\_VIEW | BEFÖRDERUNGEN |
    | SH\_PRODUCTS\_VIEW | PRODUKTE |
    
4.  Klicken Sie auf die Edge-Tabelle **SH\_SALES\_VIEW\_SH\_CUSTOMERS\_VIEW**.
    
    Wie Sie aus den Informationen **Quellscheitel** und **Zielscheitel** sehen können, ordnet dieser Achsentyp alle Beziehungen von **SH\_SALES\_VIEW** zu **SH\_CUSTOMERS\_VIEW** zu. Mit anderen Worten, es modelliert **gekaufte** Beziehungen. Standardmäßig gab der Modellierer diesem Edge-Typ das Label **SH\_SALES\_VIEW\_SH\_CUSTOMERS\_VIEW**.
    
    **Hinweis**: Wenn die Edge-Tabelle nicht angezeigt wird, können Sie die Größe des oberen Bereichs ändern. Verwenden Sie den Splitter (die horizontale Linie mit drei Punkten `...`, die beide Bereiche trennen), um die Größe zu erhöhen. Klicken Sie auf den Splitter und ziehen Sie ihn nach unten oder oben.
    
5.  Benennen Sie das Edge Label in **TO\_CUSTOMER** um:
    
    ![Endergebnis der Änderungen an der Edge-Tabelle TO_CUSTOMER](./images/model-to-customer.png "Endergebnis der Änderungen an der Edge-Tabelle TO_CUSTOMER")
    
6.  Wiederholen Sie den Vorgang für alle anderen Edge-Tabellen:
    

| Aktueller Kantenname | Umbenanntes Kantenlabel |
| --- | --- |
| SH\_SALES\_VIEW\_SH\_TIMES\_VIEW | DATE\_OF\_SALE |
| SH\_SALES\_VIEW\_SH\_PROMOTIONS\_VIEW | USING\_PROMOTION |
| SH\_SALES\_VIEW\_SH\_PRODUCTS\_VIEW | PRODUCT\_SOLD |
| SH\_SALES\_VIEW\_SH\_CHANNELS\_VIEW | VIA\_CHANNEL |

7.  Klicken Sie oben links auf die Registerkarte **Quelle**.
    
    ![Modellquellansicht](./images/model-source-view.png "Modellquellansicht")
    
    Der Quellcode für dieses Modell wird angezeigt. Der Quellcode ist in der PGQL Data Definition Language-(DDL-)Syntax geschrieben. Weitere Informationen zur Sprache finden Sie in der [neuesten PGQL-Spezifikation](https://pgql-lang.org/spec/latest/#create-property-graph).
    
    Fortgeschrittene Benutzer können den Quellcode direkt bearbeiten. Änderungen werden sofort in der Designeransicht wiedergegeben und umgekehrt.
    
8.  Klicken Sie oben links auf die Registerkarte **Vorschau**.
    
    ![Modellquellseite, mit Verweis auf Vorschau-Registerkarte](./images/model-source-choose-preview.png "Modellquellseite, mit Verweis auf Vorschau-Registerkarte")
    
    Sie sehen eine visuelle Darstellung unseres Graphmodells bisher. Jeder Kreis im Diagramm stellt einen Scheiteltyp (Label) dar. Und die Kantenbeziehung im Diagramm stellt einen Randtyp (Label) zwischen den Kreisen dar. Sie können das Diagramm neu anordnen, indem Sie auf Elemente klicken und Elemente ziehen. Sie können auch mit der rechten Maustaste auf jedes Element klicken, um die Liste der darin enthaltenen Eigenschaften anzuzeigen.
    
    ![Modellvorschau](./images/model-preview.png "Modellvorschau")
    
9.  Klicken Sie oben rechts auf **Weiter**.
    
    ![Seite "Modellübersicht"](./images/model-summary-page.png "Seite "Modellübersicht"")
    
    Sie sehen eine Zusammenfassung des von uns erstellten Modells. Alle Eingabetabellen und wie diese einem Eigenschaftsdiagramm zugeordnet werden sollen.
    

## Aufgabe 4: Diagrammerstellungsjob starten

1.  Klicken Sie oben rechts auf **Diagramm erstellen**.
    
2.  Geben Sie **SH\_PGVIEW\_GRAPH** als Diagrammnamen, **SH\_MODEL** als Modellnamen ein, und geben Sie dem Diagramm optional eine Beschreibung und einige Tags an, um es später leichter zu identifizieren. Lassen Sie die Option **In Speicher laden** aktiviert. Klicken Sie dann auf **Erstellen**.
    
    ![Dialogfeld "Diagramm erstellen"](./images/model-create-graph-dialog.png "Dialogfeld "Diagramm erstellen"")
    
    Sie werden zur Seite "Jobs" umgeleitet, auf der Sie den Job zur Diagrammerstellung sehen.
    
    ![Seite "Jobs", nachdem das Diagramm erstellt wurde](./images/jobs-after-create-graph.png "Seite "Jobs", nachdem das Diagramm erstellt wurde")
    
3.  Klicken Sie auf den ausgeführten Job. Klicken Sie im Abschnitt "Details" oben rechts auf das Symbol **Logs**.
    
    ![Seite "Joblogs", auf der Sie die Logs für das sh-Diagramm anzeigen können](./images/jobs-sh-graph-see-log.png "Seite "Joblogs", auf der Sie die Logs für das sh-Diagramm anzeigen können")
    
    Dadurch wird ein Dialog mit dem Log angezeigt.
    
    ![Joblog für sh-Diagramm](./images/jobs-log-for-sh-graph.png "Joblog für sh-Diagramm")
    
    Sie können das Dialogfeld "Logs" geöffnet lassen, um den Fortschritt der Diagrammerstellung zu überwachen. Graph Studio aktualisiert die Logs automatisch alle paar Sekunden. Der Grapherstellungsjob sollte nach einigen Minuten erfolgreich sein. Nach Abschluss wird automatisch ein weiterer **In Speicher laden**\-Job gestartet.
    
    ![Prüfen Sie, ob der Job zum Laden in den Speicher gestartet wurde](./images/jobs-sh-load-into-memory-started.png "Prüfen Sie, ob der Job zum Laden in den Speicher gestartet wurde")
    
4.  Warten Sie, bis beide Jobs erfolgreich abgeschlossen wurden.
    

## Aufgabe 5: Erstelltes Diagramm und Modell prüfen

1.  Klicken Sie auf das Menüsymbol **Diagramme**.
    
2.  Klicken Sie auf das soeben erstellte Diagramm **SH\_PGVIEW\_GRAPH**.
    
    ![Vorschau des Diagramms nach Auswahl auf der Seite "Diagramme"](./images/graphs-sh-graph-details.png "Vorschau des Diagramms nach Auswahl auf der Seite "Diagramme"")
    
    Sie können eine Vorschau des Diagramms anzeigen, dessen Namen oder Metadaten bearbeiten, mit anderen teilen, in den Speicher laden oder löschen.
    
3.  Klicken Sie auf die Menüoption **Modelle**.
    
4.  Klicken Sie auf das gerade erstellte **SH-Modell**:
    
    ![Modelldetails des SH-Modells im Modellseitenbild anzeigen](./images/models-sh-model-details.png "Modelldetails des SH-Modells im Modellseitenbild anzeigen")
    
    Genau wie das Diagramm wird auch das Modell gespeichert. Sie können den Quellcode dieses Modells sehen, mit anderen teilen, seine Metadaten bearbeiten oder löschen. Sie können auch einen anderen Grapherstellungsjob aus demselben Modell starten.
    

Herzlichen Glückwunsch! Sie haben relationale Tabellen erfolgreich in ein Eigenschaftsdiagramm konvertiert. Sie können jetzt mit leistungsstarken Diagrammabfragen und Algorithmen die Beziehungen in diesen Daten analysieren.

Sie können jetzt **mit der nächsten Übung fortfahren**.

## Danksagungen

*   **Autor** - Korbi Schmid, Produktentwicklung
*   **Mitwirkende** - Jayant Sharma, Rahul Tasker, Produktmanagement
*   **Zuletzt aktualisiert am/um** - Jayant Sharma, Juni 2023