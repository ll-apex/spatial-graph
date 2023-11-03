# Graph Studio : charger des données à partir de fichiers CSV dans des tables

## Présentation

Au cours de cet atelier, vous allez charger deux fichiers CSV dans les tables correspondantes à l'aide de l'interface Database Actions de votre instance Oracle Autonomous Data Warehouse ou Oracle Autonomous Transaction Processing.

Temps estimé : 10 minutes.

Regardez la vidéo ci-dessous pour une présentation rapide du laboratoire.

[](youtube:wkKKO-RO0lA)

### Objectifs

Découvrez comment :

*   Charger des fichiers CSV dans une instance Autonomous Database à l'aide de Database Actions

### Prérequis

*   L'exercice suivant requiert un compte Oracle Autonomous Database.
*   Il suppose qu'il existe un utilisateur compatible Graph et Web-Access. En d'autres termes, un utilisateur de base de données doté des rôles et privilèges appropriés existe et peut se connecter à Database Actions.

## Tâche 1 : connexion à Database Actions pour votre instance Autonomous Database

1.  Ouvrez la page de détails du service pour votre instance Autonomous Database dans la console Oracle Cloud.
    
    ![Le texte ALT n'est pas disponible pour cette image](images/open-database-actions.png " ")
    
2.  Cliquez sur **Database Actions** pour l'ouvrir.
    

## Tâche 2 : connectez-vous en tant qu'utilisateur compatible avec les graphiques.

1.  Connectez-vous en tant qu'utilisateur de graphique (par exemple, `GRAPHUSER`) pour votre instance Autonomous Database.
    
    ![Le texte ALT n'est pas disponible pour cette image](./images/db-actions-graphuser-login.png " ")
    
    > **Remarque :** _Si nécessaire, procédez comme suit pour créer l'utilisateur avec les rôles et privilèges appropriés_ :
    
    *   Connectez-vous à Database Actions en tant qu'utilisateur **ADMIN** pour votre instance Autonomous Database.
    *   Sélectionnez **Administration**, puis **Database Users** (Utilisateurs de base de données) dans le menu de navigation.
    *   Cliquez sur **Créer un utilisateur**.
    *   Activez les boutons **Accès au Web** et **Graphique**.

## Tâche 3 : téléchargez les exemples de jeux de données à partir de ObjectStore

1.  Copiez et collez l'URL dans votre navigateur pour l'archive zip, c'est-à-dire
    
        <copy>
        https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
    
    Ou utilisez `wget` ou `curl` pour télécharger les données échantillon sur votre ordinateur.  
    Voici un exemple de demande `curl` que vous pouvez copier et coller :
    
        <copy>
        curl -G -o acct-txn-data.zip https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
2.  **Décompressez** l'archive dans un répertoire local tel que ~/downloads.
    

## Tâche 4 : Charger à l'aide du chargement de données Database Actions

1.  Cliquez sur la carte **DATA LOAD**.
    
    ![Le texte ALT n'est pas disponible pour cette image](images/db-actions-dataload-card.png " ")
    
    Indiquez ensuite l'emplacement de vos données. Autrement dit, assurez-vous que les cartes **LOAD DATA** et **LOCAL FILE** sont cochées. Cliquez sur **Suivant**.
    
    ![Le texte ALT n'est pas disponible pour cette image](./images/db-actions-dataload-location.png)
    
2.  Cliquez sur **Sélectionner des fichiers**.
    
    ![Le texte ALT n'est pas disponible pour cette image](images/db-action-dataload-file-browser.png " ")
    
    Accédez au dossier approprié (par exemple, ~/downloads/random-acct-data) et sélectionnez les fichiers `bank_accounts.csv` et `bank_txns.csv`.
    
    ![Le texte ALT n'est pas disponible pour cette image](./images/db-actions-dataload-choose-files.png " ")
    
3.  Vérifiez que les fichiers corrects ont été sélectionnés, puis cliquez sur l'icône **Run**. ![Le texte ALT n'est pas disponible pour cette image](./images/db-actions-dataload-click-run.png " ")
    
4.  Confirmez que vous souhaitez effectuer le travail de chargement des données.
    
    ![Le texte ALT n'est pas disponible pour cette image](./images/db-actions-dataload-confirm-run.png " ")
    
5.  Une fois les fichiers chargés
    
    ![Le texte ALT n'est pas disponible pour cette image](./images/dbactions-dataload-files-loaded.png " ")
    
    Cliquez sur **Terminé** pour quitter.
    
    ![Le texte ALT n'est pas disponible pour cette image](images/dbactions-click-done.png " ")
    
6.  Ouvrez à présent la feuille de calcul **SQL**. ![Le texte ALT n'est pas disponible pour cette image](./images/db-actions-choose-sql-card.png " ")
    
7.  Accédez au dossier approprié (par exemple, ~/downloads), sélectionnez le fichier `fixup.sql` et faites-le glisser dans la feuille de calcul SQL.
    
    ![Le texte ALT n'est pas disponible pour cette image](./images/db-actions-drag-drop-fixup-sql.png " ")
    
    Toutefois, si vous préférez copier-coller, le contenu de `fixup.sql` est le suivant :
    
        <copy>
        alter table bank_accounts add primary key (acct_id);
        
        alter table bank_txns add txn_id number;
        update bank_txns set txn_id = rownum;
        commit;
        
        alter table bank_txns add primary key (txn_id);
        alter table bank_txns modify from_acct_id references bank_accounts (acct_id);
        alter table bank_txns modify to_acct_id references bank_accounts (acct_id);
        
        desc bank_txns;
        
        select * from USER_CONS_COLUMNS where table_name in ('BANK_ACCOUNTS', 'BANK_TXNS');
        </copy>      
        
    
    Il effectue les tâches suivantes :
    
    *   Ajoute une contrainte de clé primaire à la table `bank_accounts`
    *   Ajoute une colonne (`txn_id`) à la table `bank_txns`
    *   Définit une valeur pour `txn_id` et valide la transaction
    *   Ajoute une contrainte de clé primaire à la table `bank_txns`
    *   Ajoute une contrainte de clé étrangère à la table `bank_txns`, indiquant que `from_acct_id` référence `bank_accounts.acct_id`
    *   Ajoute une seconde contrainte de clé étrangère à la table `bank_txns` en spécifiant que `to_acct_id` référence `bank_accounts.acct_id`
    *   Permet de vérifier que l'ajout d'une colonne `txn_id` et les contraintes
8.  Exécutez le script `fixup.sql` dans la feuille de calcul SQL.  
    ![Le texte ALT n'est pas disponible pour cette image](./images/db-actions-sql-execute-fixup.png " ")
    
9.  La sortie du script doit se présenter comme suit :
    
    ![Le texte ALT n'est pas disponible pour cette image](./images/db-actions-sql-script-output.png " ")
    
    **Passez à l'exercice suivant** pour créer un graphique à partir de ces tableaux.
    

## Accusés de réception

*   **Auteur** - Jayant Sharma, Product Management
*   **Contributeurs** - Jayant Sharma, Product Management
*   **Dernière mise à jour par/date** - Jayant Sharma, Product Management, février 2022