# Datenbankbenutzer für Spatial Studio Repository

## Einführung

In dieser Übung wird die Erstellung des Datenbankschemas erläutert, das für das Metadaten-Repository von Spatial Studio verwendet werden soll. Dieses Schema speichert die in Spatial Studio ausgeführten Aufgaben, wie die Definitionen von Datasets, Analysen und Projekten.

Das Datenbankschema für das Repository von Spatial Studio kann technisch einen beliebigen Namen haben. Aus Konsistenzgründen mit anderen Spatial Studio-Workshops nennen wir den Benutzernamen **studio\_repo**. Beachten Sie, dass es sich hierbei um einen Datenbankbenutzernamen handelt, der sich von den Benutzernamen der Spatial Studio-Anwendung unterscheidet, z.B. dem Standardbenutzernamen des Spatial Studio-Administrators (studio\_admin), der bei der Installation der Spatial Studio-App selbst erstellt wird.

Geschätzte Laborzeit: 5 Minuten

### Ziele

*   Erfahren Sie, wie Sie ein Schema für das Spatial Studio-Metadaten-Repository erstellen
*   Erfahren Sie, wie Sie Wallet für die Datenbankverbindung herunterladen

### Voraussetzungen

*   Free Tier-, Cloud-Account vom Typ "Immer kostenlos", "Kostenpflichtig" oder LiveLabs von Oracle
*   Zugriff auf die Datenbank "SQL Developer Web".

## Aufgabe 1: Repository-Schema erstellen

1.  Stellen Sie in SQL Developer Web eine Verbindung zur autonomen Datenbank her, die für das Spatial Studio-Repository als **Admin**\-Benutzer verwendet werden soll.
    
2.  Erstellen Sie das Schema für das Spatial Studio-Repository. Das Schema kann einen beliebigen Namen haben. Zur Konsistenz mit anderen Übungen verwenden wir jedoch den Namen **studio\_repo**. Passwortanforderungen für Oracle Autonomous Database finden Sie [hier](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/manage-users-create.html#GUID-72DFAF2A-C4C3-4FAC-A75B-846CC6EDBA3F). Notieren Sie sich das ausgewählte Kennwort. Sie werden es in späteren Schritten verwenden.
    
        <copy>CREATE USER studio_repo
        IDENTIFIED BY <password goes here>;</copy>
        

## Aufgabe 2: Tablespace Quota zuweisen

1.  Weisen Sie dem Repository-Schema von Spatial Studio einen Default Tablespace zu. Mit Autonomous Database können Sie Tablespace-Namen **Daten** verwenden
    
        <copy>ALTER USER studio_repo
        DEFAULT TABLESPACE data;</copy>
        
2.  Tablespace Quota dem Repository-Schema von Spatial Studio zuweisen Die Metadaten von Spatial Studio belegen einen sehr geringen Speicherplatz. Die Quota berücksichtigt also hauptsächlich Geschäftsdaten, die im Repository-Schema gespeichert sind. Für diese Übung ist der Quota-Wert **250M** in Ordnung. Sie können den Wert auch auf **unbegrenzt** setzen, wenn Sie mit anderen Datasets experimentieren.
    
        <copy>ALTER USER studio_repo
        QUOTA <quota value> ON data;</copy>
        

## Aufgabe 3: Berechtigungen erteilen

1.  Erteilen Sie dem Spatial Studio-Repository-Schemabenutzer die folgenden Berechtigungen
    
        <copy>
        GRANT CONNECT,
              CREATE SESSION,
              CREATE TABLE,
              CREATE VIEW,
              CREATE SEQUENCE,
              CREATE PROCEDURE,
              CREATE SYNONYM,
              CREATE TYPE,
              CREATE TRIGGER
        TO  studio_repo
        </copy>
        

Das studio\_repo-Schema kann jetzt als Spatial Studio-Repository verwendet werden.

## Aufgabe 4: Wallet herunterladen

Für Spatial Studio ist ein Wallet erforderlich, um eine Verbindung zum von uns erstellten Autonomous Database-Repository-Schema herzustellen. Wir werden die Brieftasche in der nächsten Übung verwenden.

1.  Navigieren Sie zu Autonomous Database, und wählen Sie "View Details" aus.
    
    ![Alternativer Bildtext](images/repo-schema-1.png "Bildtitel")
    
2.  Wählen Sie die Registerkarte "DB-Verbindung"
    
    ![Alternativer Bildtext](images/repo-schema-2.png "Bildtitel")
    
3.  Klicken Sie auf "Download Wallet". ![Alternativer Bildtext](images/repo-schema-3.png "Bildtitel")
    
    Sie werden aufgefordert, ein Kennwort für die Wallet-Datei einzugeben. Das Wallet ist eine einzelne ZIP-Datei.
    
4.  Speichern Sie die Wallet-Datei an einem geeigneten Speicherort. Diese Datei benötigen Sie in der nächsten Übung.
    

Sie können jetzt [mit der nächsten Übung fortfahren](#next).

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Zuletzt aktualisiert am/um** - David Lapp, Database Product Management, März 2023