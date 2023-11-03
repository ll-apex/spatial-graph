# Présentation

## A propos d'Oracle Spatial

La mission d'Oracle est d'aider les gens à voir les données de nouvelles façons, à découvrir des informations et à débloquer des possibilités infinies. L'analyse spatiale consiste à comprendre les interactions complexes basées sur les relations géographiques - répondre aux questions en fonction de l'emplacement des personnes, des actifs et des ressources. Les informations spatiales vous permettent de fournir un meilleur service client, d'optimiser votre personnel, de localiser les centres de vente et de distribution, d'évaluer les campagnes de vente et de marketing, etc. Grâce aux offres spatiales d'Oracle, les développeurs, les professionnels des bases de données et les analystes peuvent utiliser une suite complète d'outils de gestion, d'analyse et de visualisation des données spatiales pour intégrer l'analyse et la mise en correspondance spatiales aux applications de l'infrastructure de gestion des données d'entreprise : Oracle Database et Oracle Exadata. Les technologies innovantes d'Oracle Cloud et d'Oracle Autonomous Database, la seule base de données du secteur dotée de fonctions d'autopilotage, d'autosécurisation et d'autoréparation, sont disponibles pour les applications spatiales.

Comme illustré ci-dessous, les fonctionnalités spatiales d'Oracle Database fournissent un stockage, un traitement et une analyse évolutifs et performants des types de données spatiales de base et avancés. Une série de composants Java EE déployables sont également fournis pour prendre en charge les services de niveau intermédiaire communs.

![texte alt img](./images/spatial-platform.png)

Pour plus d'informations, veuillez visiter \[https://oracle.com/goto/spatial\] (https://oracle.com/goto/spatial)

Durée estimée de l'atelier : 60 minutes

### Présentation de Workshop

Dans cet atelier, vous allez créer, configurer et analyser des données spatiales. Vous allez créer et configurer des tables spatiales pour STORES, WAREHOUSES, REGIONS et TORNADO\_PATHS à partir de formats courants, puis effectuer des requêtes spatiales pour explorer leurs relations en fonction de la proximité et du confinement. Vous pouvez enfin transformer les résultats à l'aide de la prise en charge native de JSON dans ADB, pour l'intégration des développeurs.

La possibilité de relier des informations basées sur l'emplacement, telles que les données relatives basées sur la proximité spatiale et le confinement, est extrêmement précieuse dans une myriade de scénarios. Aucune clé préexistante n'associe les emplacements de magasin à un entrepôt. Mais Spatial permet de déterminer une telle relation en fonction de la proximité. De même, il n'existe aucune relation préexistante entre les lieux de magasin et les régions, par exemple les régions fiscales. Mais Spatial permet de déterminer leur relation en fonction du confinement. Plus loin, Spatial permet des analyses basées sur la localisation, telles que la synthèse d'informations en fonction de la proximité, par exemple la perte due à des tornades à distance d'un emplacement. Au lieu d'effectuer ces analyses dans un système distinct, vous pouvez tirer parti des fonctionnalités spatiales intégrées d'ADB.

Vous acquerrez de l'expérience avec toutes les capacités mentionnées ci-dessus dans cet atelier.

### Prérequis

\- Un compte Oracle Cloud \- Cet atelier nécessite l'accès à un client Oracle Database et SQL (par exemple, SQL Developer, SQL Developer Web, SQL\*Plus). - Si vous avez déjà accès à ces informations, vous pouvez passer directement à la section Créer des exemples de données. - Sinon, vous devez passer aux sections Compte Oracle Cloud, Autonomous Database et SQL Developer Web. - Aucune expérience préalable avec Oracle Spatial n'est requise. - Un compte Oracle Cloud

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Contributeurs** - Karin Patenge, Gestion des produits de base de données, Oracle
*   **Dernière mise à jour par/date** - David Lapp, septembre 2022