# Accéder à Spatial Studio

## Présentation

Cet atelier explique comment accéder à Oracle Spatial Studio (Spatial Studio) à partir d'une réservation Oracle LiveLabs. Votre environnement inclut Spatial Studio et une instance Autonomous Database. Lors de la première connexion à Spatial Studio, vous fournissez les informations de connexion à votre instance Autonomous Database.

Temps de laboratoire estimé : 10 minutes

### Objectifs

Dans cet exercice, vous allez :

*   Téléchargement du portefeuille cloud pour Autonomous Database
*   Effectuer une 1ère connexion à Spatial Studio avec les informations de connexion à Autonomous Database

### Prérequis

*   Réservation LiveLabs terminée pour "Introduction à Oracle Spatial Studio"

## Tâche 1 : téléchargement du portefeuille cloud pour votre instance Autonomous Database

1.  Dans Détails de l'atelier, notez votre nom utilisateur cloud, votre mot de passe, votre compartiment et votre adresse IP Spatial Studio. Lancez ensuite la console cloud.

![Texte de remplacement de l'image](images/1-1.png "Titre de l'image")

2.  Connectez-vous à l'aide de la **connexion directe Oracle Cloud Infrastructure** à l'aide de votre nom utilisateur cloud et de votre mot de passe initial. Vous serez invité à modifier le mot de passe par défaut.

![Texte de remplacement de l'image](images/1-2.png "Titre de l'image")

3.  Accédez à **Oracle Database**, puis à **Autonomous Database**.

![Texte de remplacement de l'image](images/1-3.png "Titre de l'image")

4.  Dans le formulaire Compartiment à gauche, commencez à saisir le nom de compartiment indiqué précédemment. Cette opération filtre dynamiquement la liste Compartiments. Une fois répertorié, sélectionnez votre compartiment. Votre instance Autonomous Database sera alors répertoriée. Cliquez sur le lien vers votre instance Autonomous Database.

![Texte de remplacement de l'image](images/1-4.png "Titre de l'image")

5.  Cliquez sur **Connexion à la base de données**, puis sur **Télécharger le portefeuille**. Vous serez promu pour un mot de passe de portefeuille. Entrez une chaîne car ce mot de passe ne sera pas utilisé. Enregistrez le portefeuille à un emplacement pratique sur votre ordinateur portable, car vous l'utiliserez à l'étape suivante.

![Texte de remplacement de l'image](images/1-5.png "Titre de l'image")

## Tâche 2 : première connexion à Spatial Studio

1.  Vous allez maintenant utiliser l'adresse IP de Spatial Studio que vous avez indiquée précédemment. Ouvrez un nouvel onglet dans votre navigateur et accédez à **https ://\[votre adresse IP Spatial Studio\] :4040/spatialstudio**. Par exemple, si votre adresse IP Spatial Studio est 123.123.12.123, vous accédez à https://123.123.12.123:4040/spatialstudio.. Votre instance Spatial Studio n'étant pas configurée avec un certificat SSL signé, un avertissement de sécurité propre au navigateur s'affiche. Acceptez l'avertissement et accédez au site. Dans un environnement de production, un certificat est configuré et cela ne se produit pas. Connectez-vous avec l'utilisateur **admin** et le mot de passe **welcome1**.

![Texte de remplacement de l'image](images/2-1.png "Titre de l'image")

2.  La première connexion à Spatial Studio vous invite à saisir les informations de connexion à la base de données pour le référentiel de métadonnées de Spatial Studio. Cliquez sur **Autonomous Database**, puis sur **Suivant**. Sur la séquence suivante, glissez-déplacez le fichier de portefeuille que vous avez téléchargé précédemment et cliquez sur **OK**.

![Texte de remplacement de l'image](images/2-2.png "Titre de l'image")

3.  Vous êtes maintenant invité à saisir les informations de connexion à la base de données Automomous. Entrez l'utilisateur **studio\_repo**, le mot de passe **Welcome1Welcome1** et sélectionnez le niveau de service moyen.

![Texte de remplacement de l'image](images/2-3.png "Titre de l'image")

Spatial Studio est en train de créer ses tables de métadonnées dans Autonomous Database. Cela prendra environ 30 secondes.

4.  Lorsque Spatial Studio s'ouvre, la première connexion est terminée et vous êtes prêt à poursuivre l'atelier.

![Texte de remplacement de l'image](images/2-4.png "Titre de l'image")

Vous pouvez maintenant [passer à l'exercice suivant](#next).

## En savoir plus

*   [Page produit Spatial Studio](https://oracle.com/goto/spatialstudio)

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management
*   **Dernière mise à jour par/date** - David Lapp, Database Product Management, juin 2021