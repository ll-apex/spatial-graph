# Bereinigen

## Einführung

In dieser Übung heben Sie das Deployment der Spatial Studio-Instanz auf, die mit dem Cloud Marketplace erstellt wurde. Alle Ressourcen, die im Rahmen der Spatial Studio-Bereitstellung erstellt wurden, werden endgültig aus dem Cloud Marketplace gelöscht.

Geschätzte Laborzeit: 5 Minuten

Sehen Sie sich das Video unten an, um einen schnellen Durchgang des Labors zu erhalten.

[Bereinigungsoption 2: Spatial Studio und ADB beenden](videohub:1_1jnminp7)

### Ziele

In dieser Übung führen Sie folgende Schritte aus:

*   Heben Sie das Deployment von Spatial Studio und zugehörigen Ressourcen auf, die über den Oracle Cloud Marketplace erstellt wurden.

### Voraussetzungen

*   Spatial Studio, das über den Cloud Marketplace bereitgestellt wird

## Aufgabe 1: Bereitgestellte Ressourcen löschen

Navigieren Sie zu dem Stack, mit dem Sie die Spatial Studio-Instanz erstellen.

1.  Navigieren Sie zu **Entwicklerservices > Stacks**.
    
    ![Navigieren Sie zu Stacks in der OCI-Konsole](images/teardown-01.png)
    
2.  Wählen Sie im Aktionsmenü Ihres Stacks die Option **Stackdetails anzeigen** aus.
    
    ![Stackdetails anzeigen](images/teardown-02.png)
    
3.  Klicken Sie auf **Zerstören**. Dadurch werden die vom Spatial Studio Marketplace-Deployment erstellten Ressourcen gelöscht.
    
    ![Stack zerstören](images/teardown-03.png)
    
4.  Bestätigen Sie dies, indem Sie erneut auf **Zerstören** klicken.
    
    ![Löschen des Stacks bestätigen](images/teardown-04.png)
    
5.  Warten Sie etwa 3-4 Minuten, bis der Prozess abgeschlossen ist. Beachten Sie den Status im Abschnitt "Jobs". Wenn der Status **Erfolgreich** lautet, ist die Arbeitslosigkeit abgeschlossen, und alle Ressourcen, die vom Spatial Studio Marketplace-Deployment bereitgestellt werden, werden gelöscht.
    
    ![Löschjob prüfen](images/teardown-05.png)
    

## Aufgabe 2: Stack löschen (optional)

Der Stack ist das Set von Anweisungen für das Deployment. Es erfasst die Einstellungen, die Sie beim Ausführen des Cloud Marketplace-Assistenten ausgewählt haben. Nachdem Sie Ressourcen gelöscht haben, die beim Ausführen des Stacks zum Erstellen der Spatial Studio-Instanz erstellt wurden, können Sie jetzt den Stack selbst löschen. Nachdem Sie den Stack gelöscht haben, müssen Sie mit dem Cloud Marketplace neu beginnen, um Spatial Studio erneut bereitzustellen. Sie können den Stack auch unverändert beibehalten und erneut ausführen oder ihn bearbeiten, um Parameter wie das Hinzufügen eines SSH-Schlüssels zum Erstellen einer längerfristigen Instanz zu ändern.

1.  Wählen Sie im Menü **Weitere Aktion** des Stacks die Option **Stack löschen** aus.
    
    !["Stack löschen" auswählen](images/teardown-06.png)
    
2.  Wenn Sie zur Bestätigung aufgefordert werden, klicken Sie auf **Löschen**.
    
    ![Löschen von Stack bestätigen](images/teardown-07.png)
    
3.  Alle vom Cloud Marketplace-Assistenten erstellten Artefakte, sowohl Ressourcen als auch der Stack, sind jetzt verschwunden.
    

## Weitere Informationen

*   [Oracle Spatial-Produktseite](https://www.oracle.com/database/spatial)
*   [Erste Schritte mit Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)
*   [Dokumentation zu Spatial Studio](https://docs.oracle.com/en/database/oracle/spatial-studio)

## Danksagungen

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Mitwirkende** - Jesus Vizcarra
*   **Zuletzt aktualisiert am/um** - David Lapp, August 2023