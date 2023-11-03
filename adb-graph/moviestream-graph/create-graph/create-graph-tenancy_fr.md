# Créer un graphe

## Présentation

Dans cet exercice, vous allez créer un graphique à partir des tables `MOVIE, CUSTOMER\_SAMPLE` et `WATCHED` à l'aide de l'expérience utilisateur guidée Graph Studio.

Temps estimé : 15 minutes.

### Objectifs

Découvrez comment :

*   Utiliser Graph Studio pour modéliser et créer un graphique à partir de tables ou de vues existantes.

### Prérequis

*   L'exercice suivant nécessite une instance sans serveur Autonomous Database.
*   Et que l'utilisateur compatible Graph existe. En d'autres termes, il existe un utilisateur de base de données doté des rôles et privilèges appropriés.

## Tâche 1 : accéder à Autonomous Database

1.  Cliquez sur le **menu de navigation** en haut à gauche, accédez à **Oracle Database** et sélectionnez **Autonomous Database**.
    
    ![Accès à Autonomous Database.](images/navigation-menu.png " ")
    
2.  Sélectionnez votre **compartiment**, puis cliquez sur le **nom d'affichage** de l'instance **Autonomous Database**.
    
    ![Sélection d'Autonomous Database dans le menu de navigation.](images/select-autonomous-database.png " ")
    

## Tâche 2 : se connecter à Graph Studio

[](include:adb-goto-graph-studio.md)

## Tâche 3 : créer un graphique de recommandations de films

[](include:adb-create-graph.md)

## Accusés de réception

*   **Auteur** - Melli Annamalai, chef de produit, Oracle Spatial and Graph
*   **Contributeurs** - Jayant Sharma
*   **Dernière mise à jour par/date** - Ramu Murakami Gutierrez, chef de produit, Oracle Spatial and Graph, juillet 2023