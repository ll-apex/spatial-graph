# Présentation

## A propos de cet atelier

Dans cet atelier, vous allez explorer la mise en correspondance dans Oracle APEX à l'aide de la fonctionnalité Map Region et d'Oracle Spatial. Vous installerez et explorerez un exemple d'application prédéfini avec de nombreux exemples de mappage utiles. Vous allez ensuite créer votre propre application avec et configurer des cartes à la fois à l'aide d'un assistant et à partir de zéro.

La région de carte est une fonctionnalité APEX native introduite dans APEX 21.1 qui permet de configurer des cartes interactives affichant des données spatiales d'Oracle Spatial, GeoJSON et des coordonnées. Cet atelier se concentre sur l'utilisation d'Oracle Spatial comme source de données spatiales, afin que les données spatiales brutes et les résultats d'analyse spatiale soient facilement incorporés.

![Application de cartes échantillon](./images/intro-01.png "Oracle Application Express - Exemple d'application Maps ")

Durée estimée de l'atelier : 1 heure 15 minutes

### A propos d'Oracle Application Express (APEX) et d'Oracle Spatial

Oracle Application Express (APEX) et Oracle Spatial sont des fonctionnalités d'Oracle Database, y compris les services Autonomous Data Warehouse (ADW) et Autonomous Transaction Processing (ATP).

Oracle Application Express (APEX) est une plate-forme de développement low-code qui vous permet de construire des applications d'entreprise évolutives et sécurisées dotées de fonctionnalités de premier ordre et pouvant être déployées partout dans le monde. Plus d'informations sur la [page d'accueil du produit Oracle APEX](https://apex.oracle.com)

Oracle Spatial est un ensemble de fonctionnalités de gestion, d'analyse et de traitement des données géospatiales au sein d'Oracle Database. Avec un type de données spatiales natif et des opérations d'analyse, l'analyse basée sur la localisation est traditionnelle et colocalisée avec toutes les autres opérations de base de données. Pour en savoir plus, consultez la [page d'accueil des produits Oracle Spatial](https://www.oracle.com/database/spatial)

### Objectifs

*   Comprendre les exemples de région de carte APEX
*   Apprendre à créer et configurer une région de carte
*   Apprenez à intégrer l'analyse de localisation à Oracle Spatial

### Prérequis

*   Oracle APEX 21.1+ est requis. Les captures d'écran de cet atelier sont réalisées à l'aide d'APEX 21.2. Etant donné que nous recommandons généralement d'utiliser la [dernière version d'APEX](https://www.oracle.com/tools/downloads/apex-downloads/), attendez-vous à de petites différences occasionnelles dans l'interface utilisateur.
*   Une expérience de base avec Oracle APEX est recommandée, mais pas requise. Si nécessaire, consultez l'atelier d'introduction LiveLabs APEX suivant : [Création d'une application basée sur des tables existantes pour Oracle Autonomous Cloud Service](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=628).
*   Une expérience de base avec Oracle Spatial est recommandée, mais n'est pas requise. Si nécessaire, consultez l'atelier d'introduction LiveLabs Spatial suivant : [Introduction à Oracle Spatial](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=736)

_Remarque : si vous disposez d'un compte **Essai gratuit**, à l'expiration de votre période d'évaluation gratuite, votre compte sera converti en compte **Toujours gratuit**. Vous ne pourrez pas organiser d'ateliers Free Tier à moins que l'environnement Always Free ne soit disponible. **[Cliquez ici pour accéder à la page FAQ sur le niveau gratuit.](https://www.oracle.com/cloud/free/faq.html)**_

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Contributeurs** - Jayson Hanes, APEX Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, mars 2023