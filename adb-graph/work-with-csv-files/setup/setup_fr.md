# Configuration : exécuter la pile

## Présentation

Dans cet atelier, vous allez créer une pile qui exécutera un script terraform pour générer une instance Autonomous Database, créer un utilisateur de graphique et télécharger l'ensemble de données qui sera utilisé.

Durée estimée : 5 minutes.

Regardez la vidéo ci-dessous pour une présentation rapide du laboratoire. [Procédure pas à pas](videohub:1_4lr4x8eb)

### Objectifs

Découvrez comment :

*   Exécutez la pile pour créer une instance Autonomous Database, un utilisateur de graphique et télécharger l'ensemble de données
*   Connexion à Graph Studio

## Tâche 1 : créer un compartiment OCI

[](include:iam-compartment-create-body.md)

## Tâche 2 : exécuter la pile

Les instructions ci-dessous vous montreront comment exécuter une pile qui créera automatiquement une instance Autonomous Database contenant un utilisateur de graphique et l'ensemble de données requis pour les requêtes de graphique de propriétés.

1.  Connectez-vous à Oracle Cloud.
    
2.  Une fois connecté, utilisez ce [lien](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oracle-quickstart/oci-arch-graph/releases/latest/download/orm-graph-stack.zip) pour créer et exécuter la pile.
    
    > Remarque : le lien s'ouvrira dans un nouvel onglet ou une nouvelle fenêtre.
    
3.  Vous allez être dirigé vers cette page :
    
    ![Page Créer une pile](./images/create-stack.png)
    
4.  Cochez la case "J'ai vérifié et accepté les conditions d'utilisation d'Oracle" et choisissez votre compartiment. Laissez le reste par défaut. Cliquez sur **Suivant**.
    
    ![Option permettant de vérifier et d'accepter les conditions d'utilisation d'Oracle](./images/oracle-terms.png)
    
5.  Sélectionnez le **compartiment** pour créer l'instance Autonomous Database et le type de base de données. Cliquez sur **Suivant**. Une fois que vous serez redirigé vers la page Vérifier, cliquez sur **Créer**.
    
    ![Configurer les paramètres de la pile](./images/configure-variables.png)
    
6.  Vous serez redirigé vers une page Détails du travail avec un statut initial affiché en orange. L'icône devient verte une fois le travail terminé.
    
    ![Le travail a été exécuté avec succès](./images/successful-job.png)
    
    Pour afficher des informations sur votre application, cliquez sur **Informations sur l'application**. Enregistrez le nom utilisateur et le mot de passe du graphique car vous l'utiliserez pour vous connecter à Graph Studio.
    
    ![Affichage du nom utilisateur et du mot de passe du graphique](./images/graph-username-password.png)
    

## Tâche 3 : Connexion à Graph Studio

1.  Cliquez sur **Ouvrir Graph Studio** sous Informations sur l'application. Cela ouvrira une nouvelle page. Entrez le nom utilisateur et le mot de passe du graphique fournis sous Informations sur l'application dans l'écran de connexion.
    
    ![Ouvrir Graph Studio sous Informations sur l'application](./images/login-page.png " ")
    
2.  Cliquez ensuite sur le bouton **Connexion**. Vous devriez voir la page d'accueil du studio.
    
    ![Le texte ALT n'est pas disponible pour cette image](./images/gs-graphuser-home-page.png " ")
    
    Graph Studio se compose d'un ensemble de pages accessibles à partir du menu de gauche.
    
    L'icône **Accueil** permet d'accéder à la page d'accueil.  
    La page **Graphique** répertorie les graphiques existants à utiliser dans les blocs-notes.  
    La page **Bloc-notes** répertorie les blocs-notes existants et vous permet d'en créer un.  
    La page **Modèles** permet de créer des modèles pour les visualisations de graphique.  
    La page **Travaux** répertorie le statut des travaux en arrière-plan et vous permet d'afficher le journal associé, le cas échéant.  
    

Ceci conclut ce laboratoire. **Vous pouvez maintenant passer à l'exercice suivant.**

## Accusés de réception

*   **Auteur** - Jayant Sharma, Ramu Murakami Gutierrez, Product Management
*   **Contributeurs** - Rahul Tasker, Jayant Sharma, Ramu Murakami Gutierrez, Product Management
*   **Dernière mise à jour par/date** - Ramu Murakami Gutierrez, chef de produit, juin 2023