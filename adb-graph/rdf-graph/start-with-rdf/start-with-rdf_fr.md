# Introduction aux graphiques RDF

## Présentation

Cet atelier vous explique les étapes à suivre pour commencer en téléchargeant les données RDF vers un bucket qui sera lié à Autonomous Database. Cela nécessite la copie du nom utilisateur OCI correct à partir du profil. Pour autoriser Graph Studio à accéder aux données RDF dans OCI Object Storage (à l'aide du package DBMS\_CLOUD), vous devez créer un jeton d'accès à l'aide de votre compte OCI. Il sera utilisé dans l'exercice secondaire.

Durée estimée : 5 minutes

### Objectifs

*   Charger les données RDF dans OCI Object Storage
*   Afficher votre nom utilisateur OCI
*   Générer un jeton d'accès

### Prérequis

Cet exercice suppose que vous disposez des éléments suivants :

*   Compte Oracle Cloud
*   Téléchargez le fichier MOVIESTREAM (moviestream\_rdf.nt) à l'aide de ce [lien](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt).

## **Tâche 1 :** téléchargement de données RDF vers OCI Object Storage

1.  Connectez-vous à la console OCI à l'aide de vos informations d'identification Oracle Cloud.
2.  Ouvrez le menu de navigation et cliquez sur Stockage. Sous Object Storage et Archive Storage, cliquez sur Buckets comme indiqué : ![Image décrivant l'emplacement de sélection du dossier buckets dans le menu](./images/buckets-folder.png)
3.  Sélectionnez un compartiment qui s'applique à votre compte OCI. ![Illustration de l'emplacement du menu déroulant Compartiment sur la page Buckets](./images/compartment-menu.png)
4.  Cliquez sur Create Bucket. Le curseur Créer un bucket s'ouvre comme indiqué : ![Image décrivant la page Créer un bucket](./images/create-bucket.png)
5.  Entrez le nom du bucket, conservez toutes les valeurs par défaut, puis cliquez sur Create. Le bucket est créé et répertorié sur la page Buckets comme indiqué : ![Illustration du résultat de la création d'un bucket](./images/bucket-result.png)
6.  Cliquez sur le lien RDF\_DATA\_BUCKET et accédez à la page Détails du bucket.

![Illustration de la page Bucket après sa création](./images/bucket-page.png) 7. Cliquez sur Upload dans la section Objects. Le curseur Télécharger des objets s'ouvre. 8. Sélectionnez le [lien](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt) du fichier RDF moviestream\_rdf.nt téléchargé sur votre système local et cliquez sur Télécharger. Le fichier a été téléchargé. Cliquez sur Close (Fermer) pour revenir à la page Bucket Details (Détails du bucket). Le fichier téléchargé est répertorié sous Objects, comme indiqué : ![Illustration de l'objet téléchargé vers le bucket](./images/image-upload.png)

1.  Sélectionnez le menu Actions du fichier téléchargé et cliquez sur Visualiser les détails de l'objet pour accéder aux propriétés du fichier téléchargé. Le curseur Détails de l'objet s'ouvre comme indiqué : ![Illustration du menu Object affiché avec l'option View Object Details (Détails de l'objet vue) en surbrillance](./images/object-details.png)
2.  Notez le chemin d'URL de l'objet. Il est utilisé dans l'assistant d'importation RDF de Graph Studio. ![Image montrant où trouver le chemin d'URL de l'objet dans le bucket](./images/url-path.png)

## **Tâche 2 :** afficher votre nom utilisateur OCI

1.  Cliquez sur l'icône d'avatar dans le coin supérieur droit pour ouvrir votre profil. La première entrée sous Profil est votre nom utilisateur OCI. ![Image montrant comment accéder au profil OCI](./images/oci-profile.png)
2.  Notez le nom utilisateur OCI. Il est utilisé dans l'assistant d'importation RDF de Graph Studio. ![Illustration du nom utilisateur OCI à partir des détails utilisateur](./images/oci-username.png)

## **Tâche 3 :** génération d'un jeton d'accès à partir de la console OCI

1.  Connectez-vous à la console OCI à l'aide de vos informations d'identification Oracle Cloud.
    
2.  Cliquez sur l'icône d'avatar dans l'angle supérieur droit pour ouvrir votre profil et cliquez sur User Settings (Paramètres d'utilisateur). ![Image illustrant l'accès aux paramètres utilisateur à partir du profil](./images/user-settings.png)
    
3.  Cliquez sur les jetons d'authentification sous Resources comme indiqué : ![Image illustrant l'accès aux jetons d'authentification à partir du menu Ressources des paramètres utilisateur](./images/auth-tokens.png)
    
4.  Cliquez sur Generate Token. La boîte de dialogue Générer un jeton apparaît. ![Image illustrant la génération d'un jeton d'authentification](./images/gen-tokens.png)
    
5.  Entrez une description et cliquez sur Générer un jeton. Les détails du jeton généré sont affichés comme suit : ![Image illustrant la copie du jeton d'authentification généré](./images/token-details.png)
    
6.  Cliquez sur Copier pour copier le jeton et l'enregistrer pour une utilisation ultérieure.
    

Ceci conclut ce laboratoire. _Vous pouvez maintenant passer à l'exercice suivant._

## Accusés de réception

*   **Auteur**\- Melliyal Annamalai, Chef de produit distingué
*   **Contributeur technique** - Nicholas Cusato, Santa Monica Specialist Hub
*   **Dernière mise à jour par/date** - Nicholas Cusato, Santa Monica Specialist Hub, 25 février 2022