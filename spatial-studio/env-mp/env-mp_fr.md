# Installer Spatial Studio

## Présentation

Cet atelier parcourt le processus de provisionnement d'Oracle Spatial Studio (Spatial Studio) à l'aide d'Oracle Cloud Marketplace. Oracle Cloud Marketplace fournit des applications et services fournis par Oracle et les 3ème parties. Les détails sont disponibles [ici](https://docs.oracle.com/en/cloud/marketplace/marketplace-cloud/index.html).

Temps de laboratoire estimé : 30 minutes

### Objectifs

Dans cet exercice, vous allez :

*   Découvrez comment installer Spatial Studio à partir d'Oracle Cloud Marketplace
*   Apprendre à définir le schéma du référentiel Spatial Studio lors du lancement initial

### Prérequis

*   Un compte cloud Oracle Free Tier, Always Free, payant ou LiveLabs
*   Schéma de référentiel créé (exercice 3).

## Tâche 1 : sélectionner Spatial Studio à partir de Marketplace

1.  Cliquez sur le **menu de navigation** en haut à gauche et sélectionnez **Marketplace**.

![Oracle Cloud Marketplace ](https://oracle-livelabs.github.io/common/images/console/marketplace.png "Marché")

2.  Recherchez Spatial Studio, puis cliquez sur l'application Oracle Spatial Studio.

![Oracle Spatial Studio dans Oracle Cloud Marketplace](images/env-marketplace-2.png "Images d'Oracle Spatial Studio Marketplace")

3.  Vérifiez les instructions d'utilisation, acceptez les conditions générales et cliquez sur Lancer la pile.

![Lancer la pile pour déployer Oracle Spatial Studio](images/env-marketplace-3.png "Lancer la pile")

## Tâche 2 : Assistant Créer une pile

1.  Entrez éventuellement un nom et une description personnalisés pour la pile de déploiement. Sélectionnez ensuite le compartiment à utiliser pour le déploiement, puis cliquez sur Next.

![Créer un assistant de pile](images/env-marketplace-4.png "Créer la pile à l'aide de l'assistant")

2.  Sélectionnez Domaine de disponibilité et forme pour l'instance de calcul.

Vous trouverez des détails sur les formes de calcul [ici](https://docs.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm). Vérifiez la disponibilité des quotas de la forme souhaitée dans les domaines de disponibilité. Cette opération est particulièrement importante lors de l'utilisation d'une forme Toujours gratuit : \*Dans la console OCI, accédez à Gouvernance > Limites, quotas et utilisation \* Pour le service, sélectionnez Calcul et pour la portée, sélectionnez un domaine de disponibilité \*Confirmez la disponibilité de la forme souhaitée \* Modifiez la sélection du domaine de disponibilité si nécessaire pour identifier le quota disponible

![Limites, quotas et utilisation des ressources Oracle Cloud](images/env-marketplace-4-1.png "Limite pour les ressources de calcul")

Après avoir confirmé le quota, effectuez des sélections dans l'assistant Créer une pile.

![Définir les paramètres de pile](images/env-marketplace-5.png "Sélectionner une instance de calcul")

Ensuite, faites défiler vers le bas.

3.  Modifiez éventuellement le port HTTPS et le nom utilisateur de l'administrateur Spatial Studio à partir des valeurs par défaut. Pour l'authentification de l'administrateur Spatial Studio, vous pouvez utiliser des clés secrètes OCI Vault ou un mot de passe. L'image ci-dessous montre un exemple d'utilisation d'un mot de passe. Pour les déploiements de production, vous êtes invité à utiliser des clés secrètes OCI Vault. Faites défiler la page jusqu'à la section sur la configuration réseau.

Remarque : Par défaut, le nom utilisateur de l'administrateur Spatial Studio est **admin**. Il s'agit d'un utilisateur de l'application Spatial Studio distinct du nom utilisateur de la base de données (studio\_repo) créé dans l'exercice 3 pour le schéma de référentiel stocké dans la base de données.

![Définir d'autres paramètres, tels que le port et le mot de passe](images/env-marketplace-6.png "Configuration avancée de Spatial Studio - Mot de passe de l'administrateur Spatial Studio")

4.  Pour la mise en réseau, vous avez la possibilité de créer automatiquement un nouveau VCN ou un VCN existant. Sélectionnez le compartiment pour créer un VCN ou rechercher des réseaux cloud virtuels existants.

L'image ci-dessous montre un exemple d'utilisation de Créer un VCN. Pour utiliser un VCN existant, il doit se trouver dans le même domaine de disponibilité que celui sélectionné ci-dessus à l'étape 2. Si vous ne disposez pas d'autres réseaux cloud virtuels existants, vous pouvez conserver les valeurs par défaut restantes telles quelles. Si vous disposez d'autres réseaux cloud virtuels existants, mettez à jour les valeurs CIDR pour éviter tout conflit.

![Configurer le réseau](images/env-marketplace-7.png "Configuration avancée de Spatial Studio - Configuration réseau")

Accédez à la section des clés SSH.

5.  Le chargement d'une clé publique SSH permet d'accéder au système de fichiers de Spatial Studio à des fins d'administration. La boîte de dialogue contient des liens vers la documentation de connexion SSH générale. Soumettez votre clé publique SSH en accédant au fichier de clés ou en copiant-collant la chaîne de clé. Si vous chargez la clé publique SSH à partir d'un fichier, le nom du fichier de clés sera affiché comme indiqué dans l'image ci-dessous. Cliquez sur Next.

![Ajoutez une clé SSH.](images/env-marketplace-8.png "Configuration avancée de Spatial Studio - Clé SSH publique")

6.  Consultez le récapitulatif de vos entrées. Si des corrections sont nécessaires, cliquez sur Précédent. Sinon, cliquez sur Create pour démarrer le processus de déploiement. Vous serez redirigé vers la page Détails du travail pour le déploiement.

![Créer une pile](images/env-marketplace-9.png "Vérifier la définition de la pile et créer une pile")

## Tâche 3 : surveiller la progression du déploiement

1.  La section Journaux en bas de la page Détails du travail affiche la progression. Il affiche initialement un spinner lors de la configuration du déploiement.

![Surveiller le travail de déploiement de pile - Application de Terraform](images/env-marketplace-10.png "Surveiller la progression du déploiement de pile")

Après quelques minutes, vous verrez les informations de journal.

![Journaliser les informations sur le travail de déploiement](images/env-marketplace-11.png "Journal de déploiement de la pile")

2.  Faites défiler la page jusqu'en bas de la section des journaux. Lorsque vous avez terminé, l'application est terminée. Elle est suivie des détails de l'instance. Le dernier élément répertorié est l'URL publique de Spatial Studio. Copiez cette URL et collez-la dans un navigateur.

![Travail de déploiement terminé](images/env-marketplace-12.png "Variables de sortie pour la pile déployée")

## Tâche 4 : première connexion

1.  L'ouverture initiale de l'URL publique de Spatial Studio affiche un avertissement lié à la confidentialité et à la sécurité. L'avertissement spécifique dépend de votre plate-forme et de votre navigateur.

![Avertissement lors de l'ouverture de l'URL de Spatial Studio](images/env-marketplace-13.png "Avertissement de connexion au navigateur")

Il ne s'agit pas d'un problème de Spatial Studio ; il est générique pour accéder aux sites Web qui n'ont pas de certificat HTTPS signé. Le chargement et la configuration d'un certificat signé supprime cet avertissement. Cependant, le processus de chargement des certificats dans Jetty dépasse le cadre de cet atelier.

Cliquez sur le lien pour accéder au site Web.

2.  Entrez le nom utilisateur de l'administrateur Spatial Studio (par défaut, admin) et le mot de passe que vous avez saisi à l'étape 2 (Assistant Créer une pile, élément 3). Cliquez ensuite sur Sign In.

![Indiquez un nom d'utilisateur et un mot de passe pour vous connecter à Spatial Studio](images/env-marketplace-14.png "Boîte de dialogue de connexion à Spatial Studio")

3.  Lors de la première connexion à une instance Spatial Studio, vous êtes invité à saisir les informations de connexion du schéma de base de données à utiliser comme référentiel de métadonnées de Spatial Studio. Il s'agit du schéma de base de données utilisé pour toutes les métadonnées de Spatial Studio et peut également être utilisé par les administrateurs de Spatial Studio pour stocker d'autres données. Vous utiliserez le schéma créé à l'atelier 3. Sélectionnez Oracle Autonomous Database et cliquez sur Next.

![Choisir un type de connexion de métadonnées](images/env-marketplace-15.png "Choisir le type de référentiel de métadonnées Spatial Studio")

4.  Accédez au fichier de portefeuille enregistré dans l'atelier 3 (ou effectuez un glisser-déplacer). Après le chargement, le nom du fichier de portefeuille est répertorié en tant que portefeuille sélectionné. Cliquez sur OK.

![Télécharger le portefeuille](images/env-marketplace-16.png "Télécharger le portefeuille de connexion vers le serveur")

5.  Saisissez le nom d'utilisateur et le mot de passe définis dans l'exercice 2 et le service. Un niveau de service moyen est approprié pour cet atelier. Cliquez sur OK.

![Entrer les détails de connexion pour le référentiel de métadonnées](images/env-marketplace-17.png "Entrer les informations de connexion")

6.  Patientez quelques instants pendant que Spatial Studio établit sa connexion initiale au schéma et crée plusieurs tables de métadonnées. Lorsque vous avez terminé, Spatial Studio s'ouvre avec les informations de mise en route.

![Page d'accueil de Spatial Studio - Commencer](images/env-marketplace-18.png "Page de destination de Spatial Studio")

## Tâche 5 : charger des données et créer une correspondance

Pour vérifier que Spatial Studio fonctionne correctement, vous allez charger, préparer et visualiser un petit échantillon de données. Les données contiennent une liste de musées, y compris le nom et l'adresse. Vous géocodez les données et visualisez-les sur une carte interactive.

1.  Vous ne créerez pas de connexion ici car vous pouvez utiliser la connexion au référentiel Spatial Studio pour cette vérification. Cliquez sur la mosaïque pour **Créer un ensemble de données**.

![Démarrer l'assistant pour télécharger des données](images/verify-1.png "Créer un ensemble de données")

2.  Téléchargez le fichier d'exemple de données [ici](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/sf_area_museums.xlsx) et enregistrez-le à l'emplacement approprié. Ensuite, faites glisser le fichier vers la mosaïque de téléchargement de fichier. Vous pouvez également cliquer sur la mosaïque de chargement de fichier et accéder au fichier.

![Créer un ensemble de données en téléchargeant les données](images/verify-2.png "Charger les données de feuille de calcul existantes")

3.  Dans l'aperçu des données, définissez la connexion de téléchargement sur SPATIAL\_STUDIO et le type de données de POSTAL\_CODE sur STRING. Cliquez ensuite sur **Soumettre**.

![Indiquer les détails de téléchargement](images/verify-3.png "Indiquer les détails de téléchargement et vérifier les paramètres de colonne")

4.  Une fois le chargement terminé, l'ensemble de données est répertorié avec une icône d'avertissement indiquant que des actions doivent être effectuées. Cliquez sur l'icône d'avertissement, puis sur le lien **Accéder aux colonnes de jeu de données** pour affecter une colonne de clé.

![Définir la colonne de clé pour le jeu de données](images/verify-4.png "Résoudre les problèmes de jeu de données - choisir ou ajouter une colonne de clé")

5.  Sélectionnez NOM comme clé, puis cliquez sur **Valider la clé**.

![Valider la clé](images/verify-5.png "Valider la clé choisie")

Une fois la clé validée, cliquez sur **Appliquer**.

6.  Cliquez à nouveau sur l'icône d'avertissement, puis sur le bouton **Adresses de géocode** pour convertir les adresses en coordonnées pour la visualisation de carte.

![Adresses de géode](images/verify-7.png "Résoudre les problèmes de jeu de données - adresses de géocode")

7.  Notez que les colonnes ADDRESS et POSTAL\_CODE ont été automatiquement détectées pour une utilisation dans le géocodage. Acceptez les valeurs par défaut et cliquez sur **Appliquer**.

![Mappage des adresses de géocode](images/verify-8.png "Mapper l'ensemble de données avec les données de référence de géocodage")

Une fois le géocodage terminé, vous revenez à la page Jeux de données.

8.  Cliquez sur le menu d'actions de l'ensemble de données SF\_AREA\_MUSEUMS et sélectionnez **Créer un projet**.

![Commencez à créer le projet](images/verify-9.png "Créer un projet pour l'ensemble de données")

9.  Cliquez sur l'ensemble de données SF\_AREA\_MUSEUMS et déposez-le n'importe où sur la carte.

![Ajouter des jeux de données et les faire glisser dans le canevas de carte](images/verify-10.png "Ajouter des ensembles de données en tant que couches au projet")

L'ensemble de données SF\_AREA\_MUSEUMS sera ajouté en tant que couche de carte, et la carte effectuera un panoramique et un zoom sur la zone des données.

10.  Cliquez sur le menu d'actions de la couche SF\_AREA\_MUSEUMS et sélectionnez **Paramètres**.

![Paramètres de couche de données](images/verify-11.png "Définir des styles, etc., pour la couche de données")

11.  Stylez la couche de carte en sélectionnant la couleur et l'opacité de votre choix.

![Paramètre de style](images/verify-12.png "Sélectionner la couleur et l'opacité de la couche de données")

12.  Cliquez sur l'onglet **Interaction**, activez **Afficher la fenêtre d'informations** et sélectionnez toutes les colonnes. Cliquez ensuite sur un élément de la carte pour afficher une fenêtre d'informations contenant les valeurs de données de l'élément sélectionné.

![Paramètres pour les interactions de carte](images/verify-13.png "Définir les détails d'interaction avec la carte")

Cela permet de vérifier que la préparation et la visualisation des données de base fonctionnent correctement.

13\. Cliquez sur le bouton du panneau de navigation de gauche pour revenir à la page Jeux de données. Sélectionnez l'option **Abandonner les modifications** car vous n'avez pas besoin de conserver ce test.

![Annuler les modifications](images/verify-14.png "Annuler les modifications apportées au projet en cours")

14.  Une fois la vérification terminée, vous pouvez supprimer l'ensemble de données et la table de base de données de test. Cliquez sur le menu d'actions de SF\_AREA\_MUSEUMS et sélectionnez **Supprimer**.

![Supprimer l'ensemble de données](images/verify-15.png "Supprimer l'ensemble de données")

15.  Sélectionnez l'option de suppression de la table de base de données et cliquez sur **OK**.

![Cliquez sur cette option pour supprimer définitivement la table de base de données](images/verify-16.png "Supprimer la table de base de données associée au jeu de données")

Oracle Spatial Studio est désormais provisionné et testé. Le laboratoire suivant décrit les étapes à suivre pour démanteler Spatial Studio lorsque cela n'est plus nécessaire.

## Tâche 6 : désinstaller Spatial Studio (lorsque vous n'en avez plus besoin)

**Si vous souhaitez supprimer complètement votre déploiement Marketplace, procédez comme suit.**

1.  Cliquez sur le **menu de navigation** en haut à gauche, accédez à **Services de développeur** et sélectionnez **Piles**.

![Nettoyer toutes les ressources déployées](https://oracle-livelabs.github.io/common/images/console/developer-resmgr-stacks.png "Enlever le déploiement de Marketplace")

2.  Choisissez le compartiment et le nom utilisés dans l'étape 2. Dans l'exemple ci-dessous, un compartiment nommé Sandbox et une pile nommée Oracle Spatial Studio ont été utilisés.

![Choisissez le compartiment approprié et sélectionnez la pile à supprimer](images/env-marketplace-20.png "Sélectionner une pile")

3.  Sélectionnez Actions Terraform > Supprimer

![Détruire toutes les ressources déployées via la pile Oracle Spatial Studio](images/env-marketplace-21.png "Destruction des ressources déployées")

Vous serez invité à confirmer. Les artefacts Compute et Network créés par le déploiement Marketplace seront enlevés.

4.  Après avoir supprimé l'application Spatial Studio, votre schéma de référentiel reste en place. Pour supprimer le schéma de référentiel, connectez-vous à la base de données en tant qu'utilisateur **admin** comme indiqué à l'atelier 3 et exécutez la commande suivante.

    <copy>DROP USER studio_repo CASCADE;</copy>
    

## En savoir plus

*   [Page produit Spatial Studio](https://www.oracle.com/database/spatial/#rc30p2)
*   [Lancez-vous avec Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, Database Product Management, mars 2023