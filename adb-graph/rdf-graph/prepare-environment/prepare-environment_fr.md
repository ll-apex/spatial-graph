# Préparation de l'environnement

## Présentation

Oracle Autonomous Transaction Processing (ATP) est un service de base de données Oracle entièrement géré doté de fonctionnalités d'auto-pilotage sur Oracle Cloud Infrastructure (OCI). Il est recommandé de créer un utilisateur autorisé à utiliser Graph Studio.

Le manuel d'exercices suivant explique comment provisionner un DAV et créer un utilisateur avec des autorisations pour Graph Studio.

Temps estimé : 15 minutes

### Objectifs

*   Créez Autonomous Database sur Oracle Cloud.

### Prérequis

*   Navigateur Web
*   Assurez-vous toujours que vous êtes dans la région et le compartiment corrects

## **Tâche 1 :** connexion à Oracle Cloud

1.  Dans votre navigateur, connectez-vous à Oracle Cloud.

## **Tâche 2 :** provisionner le DAV

Provisionnez la base de données Autonomous Transaction Processing (ATP) en procédant comme suit. Vous pouvez également utiliser Autonomous Data Warehouse (ADW) de la même manière.

1.  Sélectionnez la région affectée dans l'angle supérieur droit de la console OCI.
    
2.  Dans le menu latéral en haut à gauche, sélectionnez Oracle Database, puis Autonomous Transaction Processing.
    

![Image montrant l'emplacement dans le menu pour accéder à Autonomous Transaction Processing](./images/atp.png)

3.  Cliquez sur Create Autonomous Database (Créer une base de données autonome).

![Illustration du bouton permettant de créer une base de données autonome](./images/create-adb.png)

4.  Choisissez votre compartiment.
    
5.  Saisissez un nom unique (peut-être votre nom) pour l'affichage et le nom de la base de données. Le nom d'affichage est utilisé dans l'interface utilisateur de la console pour identifier la base de données.
    

![Image montrant l'emplacement où entrer un nom unique pour la base de données](./images/unique-name.png)

6.  Assurez-vous que le type de charge de travail Transaction Processing est sélectionné.
    
7.  Entrez un mot de passe. Le nom d'utilisateur est toujours ADMIN. (Remarque : gardez à l'esprit votre mot de passe.)
    

![Image montrant où déclarer votre mot de passe](./images/password.png)

8.  Cliquez sur Create Autonomous Database (Créer une base de données autonome) en bas.
    
    Votre console montrera que ATP est en cours de provisionnement. Cette opération prend environ 2 ou 3 minutes.
    
    Vous pouvez vérifier le statut du provisionnement dans la demande de travail.
    

![Image indiquant où vérifier le statut de la base de données provisionnée](./images/status.png)

Ceci conclut ce laboratoire. _Vous pouvez maintenant passer à l'exercice suivant._

## Accusés de réception

*   **Auteur** - Nicholas Cusato (Hub spécialiste de Santa Monica)
*   **Contributeurs** - Nicholas Cusato (Hub spécialiste de Santa Monica)
*   **Dernière mise à jour par/date** - Nicholas Cusato, février 2022