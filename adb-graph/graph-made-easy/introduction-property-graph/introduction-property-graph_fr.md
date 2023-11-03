# Utiliser Graph Studio

## A propos de cet atelier

Cet atelier présente les principaux concepts de modélisation et d'analyse des données graphiques à l'aide des fonctionnalités de Graph Studio dans une instance Autonomous Database. Il vous montre comment utiliser des requêtes graphiques pour rechercher des paiements circulaires qui peuvent indiquer des transactions frauduleuses, et des algorithmes d'analyse graphique pour identifier les comptes via lesquels un grand nombre de transactions circulent. Vous allez interroger des données contenant des informations (artificielles) sur les comptes et les transactions. Vous allez commencer par créer un graphique, interroger le graphique, exécuter un algorithme d'analyse et visualiser les résultats. Une section facultative présente les concepts de graphique sémantique (RDF), couramment utilisés pour les graphiques Knowledge Graph, et vous montre comment charger des données à partir d'un format de graphique RDF standard tel que le format n-triple, et comment les interroger à l'aide de SPARQL, le langage de requête pour les graphiques RDF.

Durée estimée de l'atelier : 75 minutes

Si vous souhaitez nous regarder faire l'atelier, cliquez [ici](https://youtu.be/Ymk9TE9Q2K4).

### A propos de Graph Studio

Oracle Autonomous Database dispose de fonctionnalités qui lui permettent de fonctionner comme une base de données de graphique évolutive. Ils automatisent la création de modèles de graphique et de graphiques en mémoire à partir de tables de base de données. Ils incluent des blocs-notes et des API de développeur pour l'exécution de requêtes de graphique à l'aide de PGQL, un langage de requête de graphique de type SQL, plus de 60 algorithmes de graphique intégrés à l'aide d'API Java ou Python, et la visualisation de graphique native.

Regardez les deux vidéos suivantes pour plus d'informations sur Graph Studio. La première est une introduction aux graphes de propriétés et à leurs cas d'utilisation. La seconde est une visite guidée de l'interface Graph Studio.

[Simplification des analyses de graphe avec Autonomous Database](youtube:eCd-969hrak) Simplification des analyses de graphe avec Autonomous Database

[Autonomous Database : visite guidée de l'interface de Graph Studio](youtube:S6Q-IJcBkU0) Autonomous Database : visite guidée de l'interface de Graph Studio

### Objectifs

Dans cet atelier, vous allez :

*   Créer un graphique à l'aide de l'instruction CREATE PROPERTY GRAPH (langage de requête de graphique) de PGQL
*   Charger le graphe dans la mémoire pour analyse
*   Créer un bloc-notes
*   Interroger et visualiser le graphique à l'aide de paragraphes de bloc-notes PGQL
*   Exécuter des algorithmes graphiques et visualiser les résultats

### Prérequis

*   Compte Oracle Cloud
*   Instance Autonomous Database provisionnée sans serveur

Ceci conclut ce laboratoire. **Vous pouvez maintenant passer à l'exercice suivant.**

## Accusés de réception

*   **Auteur** - Jayant Sharma, Product Management
*   **Contributeurs** - Jayant Sharma, Product Management
*   **Dernière mise à jour par/date** - Ramu Murakami Gutierrez, chef de produit, août 2023