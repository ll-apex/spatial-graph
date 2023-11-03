# Utiliser l'analyse graphique pour recommander des films

## Présentation

Dans cet atelier, vous allez utiliser Graph Studio pour détecter et créer des communautés de clients en fonction du comportement d'affichage des films. Une fois que vous avez créé des communautés, faites des recommandations en fonction de ce que les membres de votre communauté ont regardé.

Temps estimé : 60 minutes

### A propos de Graph Studio

Oracle Autonomous Database dispose de fonctionnalités qui lui permettent de fonctionner comme une base de données de graphique de propriétés évolutive. Ils automatisent la création de modèles de graphique et de graphiques en mémoire à partir de tables de base de données. Ils incluent des blocs-notes et des API de développeur pour l'exécution de requêtes de graphique à l'aide de PGQL, un langage de requête de graphique de type SQL, et plus de 60 algorithmes de graphique intégrés, ainsi que de nombreuses visualisations, y compris la visualisation de graphique native.

Regardez la vidéo suivante qui présente les graphes de propriétés et leurs cas d'utilisation.

Simplification des analyses de graphe avec Autonomous Database

[](youtube:eCd-969hrak)

Dans cet atelier, vous allez utiliser un graphique créé à partir des tables MOVIE, CUSTOMER\_PROMOTIONS et CUSTSALES\_PROMOTIONS. MOVIE et CUSTOMER\_PROMOTIONS sont des tables de sommet (chaque ligne de ces tables devient un sommet). CUSTSALES\_PROMOTIONS connecte les deux tables. Il s'agit de la table de bordure. Chaque fois qu'un client dans CUSTOMER\_PROMOTIONS loue un film dans la table MOVIE, c'est un bord dans le graphique. Ce graphique a été créé pour être utilisé dans cet atelier.

Vous avez le choix entre plus de 60 algorithmes prédéfinis lors de l'analyse d'un graphique. Dans cet atelier, vous allez utiliser l'algorithme **SALSA personnalisé**, qui est un bon choix pour les recommandations de produits. Les sommets client sont mappés avec des _hubs_ et les films avec des _autorités_. Des scores de hub plus élevés indiquent une relation plus étroite entre les clients. Les scores d'autorité plus élevés indiquent que le sommet (ou le film) joue un rôle plus important dans l'établissement de cette proximité.

### Objectifs

Dans cet atelier, vous allez utiliser la fonctionnalité Graph Studio d'Autonomous Database pour :

*   Utiliser un bloc-notes
*   Exécuter quelques requêtes de graphique PGQL
*   Utiliser python pour exécuter SALSA personnalisé à partir de la bibliothèque d'algorithmes
*   Interroger et enregistrer les recommandations

### Prérequis

*   Compte Oracle Cloud

## Accusés de réception

*   **Auteur** - Melli Annamalai, chef de produit, Oracle Spatial and Graph
*   **Contributeurs** - Jayant Sharma
*   **Dernière mise à jour par/date** - Ramu Murakami Gutierrez, chef de produit, Oracle Spatial and Graph, février 2023