# Räumliche Abfragen

## Einführung

In dieser Übung werden grundlegende Spatial Querys in Oracle Database behandelt. Sie verwenden die in der vorherigen Übung erstellten Beispieldaten, um Artikel basierend auf Näherung und Eindämmung zu identifizieren.

Geschätzte Laborzeit: 15 Minuten

### Info zu räumlichen Abfragen

Oracle Database umfasst eine robuste Bibliothek von Funktionen und Operatoren für die räumliche Analyse. Dazu gehören räumliche Beziehungen, Messungen, Aggregationen, Transformationen und vieles mehr. Auf diese Vorgänge kann über natives SQL, PL/SQL, Java-APIs und jede andere Sprache zugegriffen werden, die mit Oracle Database kommuniziert.

### Ziele

In dieser Übung führen Sie folgende Schritte aus:

*   Identifizieren Sie BRANCHEN, die Näherungsbeziehungen zu einem LAGER haben
*   BRANCHEN mit Containment- und Näherungsbeziehungen zu einer COASTAL\_ZONE identifizieren

### Voraussetzungen

*   Abschluss der vorherigen Übung; Beispiel für räumliche Daten erstellen

## Räumliche Abfragen

Räumliche Abfragen in Oracle Database sind genau wie alle anderen herkömmlichen Abfragen, die Sie gewohnt sind. Der einzige Unterschied ist eine Reihe von räumlichen Funktionen und Operatoren, die Ihnen wahrscheinlich neu sind.

**Identifizieren Sie 5 nächstgelegene Niederlassungen zum Dallas Warehouse:**

    <copy> 
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5'
        ) = 'TRUE';
    </copy>
    

![Spatial Query ausführen](images/query1.png) Hinweise:

*   Der Operator `SDO_NN` gibt die "n nächsten" Verzweigungen zum Dallas Warehouse zurück, wobei "n" der für `SDO_NUM_RES` spezifische Wert ist. Das erste Argument für `SDO_NN` (`B.GEOMETRY` im obigen Beispiel) ist die zu durchsuchende Spalte. Das zweite Argument (`W.GEOMETRY` im obigen Beispiel) ist der Speicherort, an dem Sie die Nachbarn am nächsten suchen möchten. Über die Reihenfolge der zurückgegebenen Ergebnisse sollten keine Annahmen getroffen werden. Beispiel: Die erste zurückgegebene Zeile ist nicht garantiert die nächste. Wenn zwei oder mehr Filialen gleich weit vom Warehouse entfernt sind, können sie bei nachfolgenden Aufrufen an `SDO_NN` zurückgegeben werden.
*   Wenn Sie den Parameter `SDO_NUM_RES` verwenden, werden keine anderen Kriterien in der Klausel `WHERE` verwendet. `SDO_NUM_RES` berücksichtigt nur Näherungswerte. Beispiel: Wenn Sie der Klausel `WHERE` ein Kriterium hinzugefügt haben, weil die fünf nächsten Verzweigungen eine bestimmte Postleitzahl haben sollen und vier der fünf nächsten Verzweigungen eine andere Postleitzahl haben sollen, gibt die obige Abfrage eine Zeile zurück. Dieses Verhalten ist spezifisch für den Parameter `SDO_NUM_RES`. In einer unten stehenden Abfrage verwenden Sie einen alternativen Parameter für das Szenario zusätzlicher Abfragekriterien.

**Identifizieren Sie 5 nächstgelegene Niederlassungen zum Dallas Warehouse mit Entfernung:**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5 unit=km', 1
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Spatial Query ausführen](images/query2.png) Hinweise:

*   Der Operator `SDO_NN_DISTANCE` ist ein Hilfsoperator für den Operator `SDO_NN`. Er kann nur im Operator `SDO_NN` verwendet werden. Das Argument für diesen Operator ist eine Zahl, die mit der als letztes Argument von `SDO_NN` angegebenen Zahl übereinstimmt. In diesem Beispiel ist es 1. Es gibt keine versteckte Bedeutung für dieses Argument, es ist einfach ein Tag. Wenn `SDO_NN_DISTANCE()` angegeben ist, können Sie die Ergebnisse nach Entfernung sortieren und sicherstellen, dass die erste zurückgegebene Zeile die nächste ist. Wenn die Daten, die Sie abfragen, als Längen- und Breitengrad gespeichert werden, ist die Standardeinheit für `SDO_NN_DISTANCE` Meter.
*   Der Operator `SDO_NN` verfügt außerdem über einen Parameter `UNIT`, der die von `SDO_NN_DISTANCE` zurückgegebene Maßeinheit bestimmt.
*   Die Klausel `ORDER BY DISTANCE` stellt sicher, dass die Entfernungen in der Reihenfolge zurückgegeben werden, wobei der kürzeste Abstand zuerst angegeben wird.

**Identifizieren Sie 5 nächstgelegene WHOLESALE-Filialen zum Dallas Warehouse mit Entfernung:**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND B.BRANCH_TYPE = 'WHOLESALE'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_batch_size=5 unit=km', 1
        ) = 'TRUE'
        AND ROWNUM <= 5
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Spatial Query ausführen](images/query3.png) Hinweise:

*   `SDO_BATCH_SIZE` ist ein optimierbarer Parameter, der sich auf die Performance Ihrer Abfrage auswirken kann. `SDO_NN` berechnet intern diese Anzahl von Entfernungen gleichzeitig. Der anfängliche Zeilenbatch erfüllt möglicherweise nicht die Constraints in der WHERE-Klausel. Daher wird die von `SDO_BATCH_SIZE` angegebene Zeilenanzahl kontinuierlich zurückgegeben, bis alle Constraints in der WHERE-Klausel erfüllt sind. Wählen Sie eine `SDO_BATCH_SIZE`, die zunächst die Anzahl der Zeilen zurückgibt, die wahrscheinlich die Constraints in der WHERE-Klausel erfüllen.
*   Der Parameter `UNIT`, der im Operator `SDO_NN` verwendet wird, gibt die Maßeinheit des Parameters `SDO_NN_DISTANCE` an. Die Standardeinheit ist die den Daten zugeordnete Maßeinheit. Bei Längen- und Breitengraddaten ist der Standardwert Meter.
*   `B.BRANCH_TYPE = 'WHOLESALE' AND ROWNUM <= 5` sind die zusätzlichen Constraints in der `WHERE`\-Klausel. Die Rwnum-Klausel ist erforderlich, um die Anzahl der zurückgegebenen Ergebnisse auf 5 zu begrenzen.
*   Die Klausel `ORDER BY DISTANCE_KM` stellt sicher, dass die Entfernungen in der Reihenfolge zurückgegeben werden, wobei die kürzeste Entfernung zuerst und die Entfernungen in Meilen gemessen werden.

**Identifizieren Sie Niederlassungen innerhalb von 50km von Houston Warehouse:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE';
    </copy>
    

![Spatial Query ausführen](images/query4.png) Hinweise:

*   Das erste Argument für `SDO_WITHIN_DISTANCE` ist die zu durchsuchende Spalte. Das zweite Argument ist der Ort, von dem Sie die Entfernungen bestimmen möchten. Über die Reihenfolge der zurückgegebenen Ergebnisse sollten keine Annahmen getroffen werden. Beispiel: Die erste zurückgegebene Zeile ist nicht garantiert der Kunde, der dem Lager 3 am nächsten ist.
*   Der DISTANCE-Parameter, der im Operator `SDO_WITHIN_DISTANCE` verwendet wird, gibt den Entfernungswert an. In diesem Beispiel ist er 100.
*   Der Parameter UNIT, der im Operator `SDO_WITHIN_DISTANCE` verwendet wird, gibt die Maßeinheit des Parameters DISTANCE an. Die Standardeinheit ist die den Daten zugeordnete Maßeinheit. Bei Längen- und Breitengraddaten ist der Standardwert Meter, in diesem Beispiel Meilen.

**Identifizieren Sie Niederlassungen innerhalb von 50km von Houston Warehouse mit Entfernung:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE,
        ROUND(
            SDO_GEOM.SDO_DISTANCE(
                B.GEOMETRY, W.GEOMETRY, 0.05, 'unit=km'
            ), 2
        ) AS DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Spatial Query ausführen](images/query5.png) Hinweise:

*   Die Funktion `SDO_GEOM.SDO_DISTANCE` berechnet den Abstand zwischen Niederlassungsstandorten und dem Houston Warehouse.
*   Die ersten 2 Argumente für `SDO_GEOM.SDO_DISTANCE` sind BRANCH- und WAREHOUSE-Standorte für die Entfernungsberechnung.
*   Das dritte Argument für `SDO_GEOM.SDO_DISTANCE` ist der Toleranzwert. Die Toleranz ist ein Abrundungsfehlerwert, der von Oracle Spatial verwendet wird. Die Toleranz für Längen- und Breitengraddaten liegt in Metern. In diesem Beispiel beträgt die Toleranz 50 mm.
*   Der UNIT-Parameter, der im Parameter `SDO_GEOM.SDO_DISTANCE` verwendet wird, gibt die Maßeinheit der Entfernung an, die von der Funktion `SDO_GEOM`.`SDO_DISTANCE` berechnet wird. Die Standardeinheit ist die den Daten zugeordnete Maßeinheit. Bei Längen- und Breitengraddaten ist der Standardwert Meter. In diesem Beispiel sind es Meilen.
*   Die Klausel `ORDER BY DISTANCE_IN_MILES` stellt sicher, dass die Entfernungen in der Reihenfolge zurückgegeben werden, wobei die kürzeste Entfernung zuerst und die Entfernungen in Meilen gemessen werden.

**Bestimmen Sie Zweige in der Küstenzone:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE';
    </copy>
    

![Spatial Query ausführen](images/query6.png) Hinweise:

*   Der Operator `SDO_ANYINTERACT` akzeptiert 2 Argumente, geometry1 und geometry2. Der Operator gibt `TRUE` für Zeilen zurück, bei denen geometry1 innerhalb oder am Rand von geometry2 liegt.
*   In diesem Beispiel ist geometry1 `B.GEOMETRY`, die Verzweigungsgeometrien und geometry2 `C.GEOMETRY`, die Geometrie der Küstenzone. Die Tabelle COASTAL\_ZONE enthält nur 1 Zeile, sodass keine zusätzlichen Kriterien erforderlich sind.

**Identifizieren Sie Zweige außerhalb und innerhalb von 10 km Küstenzone:**

    <copy>
    
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_WITHIN_DISTANCE(
            B.GEOMETRY, C.GEOMETRY, 'distance=10 unit=km'
        ) = 'TRUE'
    )
    MINUS
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE'
    );
    </copy>
    

![Spatial Query ausführen](images/query7.png) Hinweise:

*   Im ersten Teil dieser Abfrage identifiziert der Operator `SDO_WITHIN_DISTANCE` BRANCHES innerhalb von 10 km von COASTAL\_ZONE. Dazu gehören BRANCHEN innerhalb der COASTAL\_ZONE.
*   Die Abfrage verwendet `MINUS`, um BRANCHES innerhalb der COASTAL\_ZONE zu entfernen, sodass nur BRACNCHES innerhalb von 10 km und außerhalb der COASTAL\_ZONE verbleiben.

## Weitere Informationen

*   \[Räumliches Produktportal\] (https://oracle.com/goto/spatial)
*   [Räumliche Dokumentation](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Spatial-Blogs](https://blogs.oracle.com/oraclespatial/)

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - Kamryn Vinson, November 2020