/\* SUPPRIMER CE FICHIER DANS LA VERSION PROCHAINE - VEUILLEZ UTILISER ADB-PROVISION-CONDITIONAL.MD FICHIER INSTEAD ET SPÉCIFIER LA VERSION QUE VOUS VOULEZ DANS VOTRE MANIFEST : { "title" :"Laboratoire 1 : Provisionner une instance ADB","description" :"Provisionnement d'une instance Autonomous Database","type" :"livelabs","filename" :"https://oracle-livelabs.github.io/adb/shared/adb-provision/adb-provision-conditional.md" }, \*/

# Provisionner une instance Autonomous Database (ADW et ATP)

## Présentation

Cet atelier vous explique les étapes à suivre pour commencer à utiliser Oracle Autonomous Database (Autonomous Data Warehouse \[ADW\] et Autonomous Transaction Processing \[ATP\]) sur Oracle Cloud. Dans cet exercice, vous allez provisionner une nouvelle instance ADW.

> **Remarque :** bien que cet exercice utilise ADW, les étapes sont identiques pour créer une base de données ATP.

Durée estimée : 5 minutes

### Objectifs

*   Découvrez comment provisionner une nouvelle instance Autonomous Database

## Tâche 1 : choisir ADW ou ATP dans le menu Services

1.  Connectez-vous à Oracle Cloud.
    
2.  Une fois connecté, vous accédez au tableau de bord des services cloud où vous pouvez voir tous les services à votre disposition. Cliquez sur le menu de navigation en haut à gauche pour afficher les options de navigation de niveau supérieur.
    
    > **Remarque :** vous pouvez également accéder directement à votre service Autonomous Data Warehouse ou Autonomous Transaction Processing dans la section **Actions rapides** du tableau de bord.
    
    ![Page Répertoire de base Oracle.](./images/Picture100-36.png " ")
    
3.  Les étapes suivantes s'appliquent de la même manière à Autonomous Data Warehouse ou Autonomous Transaction Processing. Cet atelier montre le provisionnement d'une base de données Autonomous Data Warehouse. Cliquez donc sur **Autonomous Data Warehouse**.
    
    ![Cliquez sur Autonomous Data Warehouse.](https://oracle-livelabs.github.io/common/images/console/database-adw.png " ")
    
4.  Assurez-vous que le type de charge globale est **Data Warehouse** ou **Tout** pour voir vos instances Autonomous Data Warehouse. Utilisez le menu déroulant **Portée de la liste** pour sélectionner un compartiment. Saisissez la première partie de votre nom utilisateur, par exemple `LL185` dans le champ Rechercher des compartiments pour localiser rapidement votre compartiment.
    
    ![Vérifiez le type de charge globale sur la gauche.](images/livelabs-compartment.png " ")
    
5.  Cette console indique qu'aucune base de données n'existe encore. S'il existe une longue liste de bases de données, vous pouvez filtrer la liste en fonction de l'**état** des bases de données (Disponible, Arrêté, Terminé, etc.). Vous pouvez également trier par **type de charge globale**. Ici, le type de charge globale **Data Warehouse** est sélectionné.
    
    ![Console des bases de données autonomes.](./images/Compartment.png " ")
    

## Tâche 2 : Créer l'instance ADB

1.  Cliquez sur **Create Autonomous Database** pour démarrer le processus de création d'instance.
    
    ![Cliquez sur Create Autonomous Database (Créer une base de données autonome).](./images/Picture100-23.png " ")
    
2.  L'écran **Create Autonomous Database** apparaît. Vous indiquez ainsi la configuration de l'instance.
    
    ![](./images/create-adb-screen-livelabs-default.png " ")
    
3.  Fournissez des informations de base pour la base de données autonome :
    
    *   **Choisir un compartiment :** quittez le compartiment par défaut.
    *   **Nom d'affichage :** entrez un nom mémorable pour la base de données à des fins d'affichage. Pour cet atelier, utilisez **ADW Finance Mart**.
    *   **Nom de la base de données** - Utilisez uniquement des lettres et des chiffres, en commençant par une lettre. La longueur maximale est de 14 caractères (les traits d'annulation ne sont pas initialement pris en charge). Pour cet exercice, utilisez **ADWFINANCE** et **ajoutez votre ID utilisateur**. Par exemple, si votre ID utilisateur est **LL-185**, entrez **ADWFINANCE185**
    
    ![Entrez les détails requis.](./images/Picture100-26-livelabs.png " ")
    
4.  Choisissez un type de charge globale. Sélectionnez le type de charge globale de votre base de données parmi les choix suivants :
    
    *   **Data Warehouse** - Pour cet atelier, choisissez **Data Warehouse** comme type de charge globale.
    *   **Transaction Processing** - Vous pouvez également choisir Transaction Processing comme type de charge globale.
    
    ![Choisissez un type de charge globale.](./images/Picture100-26b.png " ")
    
5.  Choisissez un type de déploiement. Sélectionnez le type de déploiement de votre base de données parmi les options suivantes :
    
    *   **Infrastructure partagée :** pour cet exercice, choisissez **Infrastructure partagée** comme type de déploiement.
    *   **Infrastructure dédiée :** vous pouvez également choisir Infrastructure dédiée comme type de déploiement.
    
    ![Choisissez un type de déploiement.](./images/Picture100-26_deployment_type.png " ")
    
6.  Configurez la base de données :
    
    *   **Toujours gratuit :** si votre compte cloud est un compte Toujours gratuit, vous pouvez sélectionner cette option pour créer une base de données autonome toujours gratuite. Une base de données toujours gratuite est fournie avec 1 CPU et 20 Go de stockage. Pour cet atelier, nous vous recommandons de ne pas cocher Always Free.
    *   **Sélectionner une version de base de données :** sélectionnez une version de base de données parmi celles qui sont disponibles.
    *   **Nombre d'OCPU :** nombre d'UC pour votre service. Pour cet exercice, indiquez **1 CPU**. Si vous choisissez une base de données Toujours gratuit, elle est fournie avec 1 CPU.
    *   **Stockage (To) :** sélectionnez votre capacité de stockage en téraoctets. Pour cet atelier, indiquez **1 To** de stockage. Sinon, si vous choisissez une base de données Toujours gratuit, elle est fournie avec 20 Go de stockage.
    *   **Redimensionnement automatique :** pour cet atelier, maintenez le redimensionnement automatique activé afin de permettre au système d'utiliser automatiquement jusqu'à trois fois plus de ressources d'UC et d'E/S pour répondre à la demande de charge globale.
    *   **Aperçu de la nouvelle base de données** - Si une case à cocher est disponible pour prévisualiser une nouvelle version de base de données, NE la sélectionnez PAS.
    
    > **Remarque :** vous ne pouvez pas augmenter/réduire une base de données autonome Toujours gratuit.
    
    ![Choisissez les autres paramètres.](./images/Picture100-26c.png " ")
    
7.  Créez des informations d'identification d'administrateur :
    
    *   **Mot de passe et mot de passe de confirmation :** indiquez le mot de passe de l'utilisateur ADMIN de l'instance de service. Le mot de passe doit répondre aux exigences suivantes :
    *   Le mot de passe doit comporter entre 12 et 30 caractères, et inclure au moins une lettre majuscule, une lettre minuscule et un caractère numérique.
    *   Le mot de passe ne peut pas contenir le nom utilisateur.
    *   Le mot de passe ne peut pas contenir de apostrophes (").
    *   Le mot de passe doit être différent des 4 derniers mots de passe utilisés.
    *   Le mot de passe ne doit pas être le même qu'il y a moins de 24 heures.
    *   Saisissez à nouveau le mot de passe pour le confirmer. Notez ce mot de passe.
    
    ![Entrez le mot de passe et confirmez-le.](./images/Picture100-26d.png " ")
    
8.  Choisissez l'accès réseau :
    
    *   Pour cet atelier, acceptez la valeur par défaut, "Secure access fromwhere".
    *   Si vous voulez autoriser le trafic uniquement à partir des adresses IP et des réseaux cloud virtuels que vous indiquez, où l'accès à la base de données à partir de toutes les adresses IP publiques ou de tous les réseaux cloud virtuels est bloqué, sélectionnez "Accès sécurisé à partir des adresses IP et des réseaux cloud virtuels autorisés uniquement" dans la zone Choisir l'accès réseau.
    *   Si vous souhaitez restreindre l'accès à une adresse privée au sein d'un VCN OCI, sélectionnez "Accès à l'adresse privée uniquement" dans la zone Choisir l'accès réseau.
    *   Si l'option "Require mutual TLS (mTLS) authentication" est sélectionnée, mTLS sera requis pour authentifier les connexions à votre instance Autonomous Database. Les connexions TLS vous permettent de vous connecter à votre instance Autonomous Database sans portefeuille, si vous utilisez un pilote léger JDBC avec JDK8 ou une version supérieure. Reportez-vous à la [documentation sur les options réseau](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/support-tls-mtls-authentication.html#GUID-3F3F1FA4-DD7D-4211-A1D3-A74ED35C0AF5) pour connaître les options permettant d'autoriser TLS ou de demander uniquement l'authentification TLS mutuelle (mTLS).
    
    ![Choisissez l'accès réseau.](./images/Picture100-26e.png " ")
    
9.  Choisissez un type de licence. Pour cet atelier, choisissez **BYOL (Bring Your Own License)**. Les deux types de licence sont les suivants :
    
    *   **Bring Your Own License (BYOL)** - Select this type when your organization has existing database licenses.
    *   **Licence incluse :** sélectionnez ce type pour vous abonner à de nouvelles licences du logiciel de base de données et au service cloud de base de données.
    
    ![Cliquez sur Create Autonomous Database (Créer une base de données autonome).](./images/Picture100-27-byol.png " ")
    
10.  Pour cet exercice, n'indiquez pas d'adresse électronique de contact. Le champ "Courriel du contact" vous permet de répertorier les contacts afin de recevoir des avis et annonces opérationnels, ainsi que des notifications de maintenance non planifiée.
    
    ![N'indiquez pas d'adresse électronique de contact.](images/contact-email-field.png)
    
11.  Cliquez sur **Create Autonomous Database**.
    
12.  Votre instance commencera le provisionnement. Dans quelques minutes, l'état passe de Provisionnement à Disponible. A ce stade, votre base de données Autonomous Data Warehouse est prête à être utilisée. Consultez les détails de votre instance ici, notamment son nom, sa version de base de données, son nombre d'OCPU et sa taille de stockage.
    

    ![Database instance homepage.](./images/Picture100-32.png " ")
    

Passez à l'_exercice suivant_.

## Pour en savoir plus

Cliquez [ici](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3) pour obtenir de la documentation sur le workflow standard d'utilisation d'Autonomous Data Warehouse.

## Accusés de réception

*   **Auteur** - Nilay Panchal, ADB Product Management
*   **Adapté pour le cloud par** - Richard Green, développeur principal, Database User Assistance
*   **Contributeurs** - Équipe d'assurance qualité Oracle LiveLabs (Jeffrey Malcolm Jr, stagiaire | Arabella Yao, Responsable produit stagiaire)
*   **Dernière mise à jour par/date** - Richard Green, février 2022