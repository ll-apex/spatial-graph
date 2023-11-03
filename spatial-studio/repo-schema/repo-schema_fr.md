# Utilisateur de base de données pour le référentiel Spatial Studio

## Présentation

Cet exercice traite de la création du schéma de base de données à utiliser pour le référentiel de métadonnées de Spatial Studio. Il s'agit du schéma qui stockera le travail effectué dans Spatial Studio, tel que les définitions des ensembles de données, des analyses et des projets.

Le schéma de base de données du référentiel de Spatial Studio peut techniquement avoir n'importe quel nom. Pour assurer la cohérence avec les autres ateliers Spatial Studio, nous nommons le nom utilisateur **studio\_repo**. Notez qu'il s'agit d'un nom d'utilisateur de base de données distinct des noms d'utilisateur de l'application Spatial Studio, tels que le nom d'utilisateur par défaut de l'administrateur Spatial Studio (studio\_admin) créé lors de l'installation de l'application Spatial Studio elle-même.

Temps de laboratoire estimé : 5 minutes

### Objectifs

*   Apprendre à créer un schéma pour le référentiel de métadonnées Spatial Studio
*   Découvrez comment télécharger un portefeuille pour la connexion à la base de données

### Prérequis

*   Un compte cloud Oracle Free Tier, Always Free, payant ou LiveLabs
*   Accès à la base de données SQL Developer Web.

## Tâche 1 : créer un schéma de référentiel

1.  Dans SQL Developer Web, connectez-vous à la base de données autonome à utiliser pour le référentiel Spatial Studio en tant qu'utilisateur **admin**.
    
2.  Créez le schéma du référentiel Spatial Studio. Le schéma peut avoir n'importe quel nom, mais pour assurer la cohérence avec les autres exercices, nous utilisons le nom **studio\_repo**. Les exigences de mot de passe pour Oracle Autonomous Database sont [ici](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/manage-users-create.html#GUID-72DFAF2A-C4C3-4FAC-A75B-846CC6EDBA3F). Notez le mot de passe que vous avez sélectionné, car nous l'utiliserons dans les étapes suivantes.
    
        <copy>CREATE USER studio_repo
        IDENTIFIED BY <password goes here>;</copy>
        

## Tâche 2 : Affecter un quota de tablespace

1.  Affectez le tablespace par défaut au schéma du référentiel Spatial Studio. Avec Autonomous Database, vous pouvez utiliser le nom de tablespace **data**
    
        <copy>ALTER USER studio_repo
        DEFAULT TABLESPACE data;</copy>
        
2.  Affectez un quota de tablespace au schéma de référentiel Spatial Studio. Les métadonnées de Spatial Studio occupent une très petite quantité de stockage. Le quota prend donc principalement en charge les données métier stockées dans le schéma de référentiel. Pour cet atelier, la valeur de quota de **250 M** convient. Vous pouvez également définir la valeur sur **unlimited** si vous allez expérimenter d'autres jeux de données.
    
        <copy>ALTER USER studio_repo
        QUOTA <quota value> ON data;</copy>
        

## Tâche 3 : octroyer des droits d'accès

1.  Accordez les droits d'accès suivants à l'utilisateur du schéma du référentiel Spatial Studio :
    
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
        

Le schéma studio\_repo est maintenant prêt à être utilisé en tant que référentiel Spatial Studio.

## Tâche 4 : télécharger le portefeuille

Un portefeuille est requis pour que Spatial Studio se connecte au schéma de référentiel Autonomous Database que nous avons créé. Nous utiliserons le portefeuille dans le prochain atelier.

1.  Accédez à votre instance Autonomous Database et sélectionnez View Details (Afficher les détails).
    
    ![Texte de remplacement de l'image](images/repo-schema-1.png "Titre de l'image")
    
2.  Sélectionnez l'onglet Connexion de base de données
    
    ![Texte de remplacement de l'image](images/repo-schema-2.png "Titre de l'image")
    
3.  Cliquez sur Télécharger le portefeuille.. ![Texte de remplacement de l'image](images/repo-schema-3.png "Titre de l'image")
    
    Vous serez invité à saisir un mot de passe pour le fichier de portefeuille. Le portefeuille est un fichier zip unique.
    
4.  Enregistrez le fichier de portefeuille à un emplacement approprié. Vous aurez besoin de ce fichier au prochain laboratoire.
    

Vous pouvez maintenant [passer à l'exercice suivant](#next).

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, Database Product Management, mars 2023