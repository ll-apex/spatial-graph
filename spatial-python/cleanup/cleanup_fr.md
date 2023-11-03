# Nettoyage

## Présentation

Vous pouvez nettoyer votre environnement d'atelier en réinitialisant votre instance Autonomous Database à l'état de pré-atelier.

Durée estimée : 2 minutes

### Objectifs

*   Réinitialiser Autonomous Database à l'état de pré-atelier

### Prérequis

*   Instance Autonomous Database active

## Tâche 1 : rétablissement d'Autonomous Database à l'état antérieur à l'atelier

1.  Exécutez la commande suivante pour enlever tous les artefacts de base de données créés dans cet atelier.
    
        <copy>
        import oracledb
        my_pwd = open('./my-pwd.txt','r').readline().strip()
        my_dsn = open('./my-dsn.txt','r').readline().strip()
        connection = oracledb.connect(user="admin", password=my_pwd, dsn=my_dsn)
        cursor = connection.cursor()
        cursor.execute("drop table transactions")
        cursor.execute("drop table locations")
        cursor.execute("drop table transaction_labels")
        cursor.execute("drop function lonlat_to_proj_geom")
        cursor.execute("delete from user_sdo_geom_metadata")
        connection.commit()
        </copy>
        

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, août 2023