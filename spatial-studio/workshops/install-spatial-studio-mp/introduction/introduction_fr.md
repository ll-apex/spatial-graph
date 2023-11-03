# Présentation

## A propos de cet atelier

Dans cet atelier, vous allez provisionner Spatial Studio vers Oracle Cloud à partir d'OCI Cloud Marketplace et préparer un schéma dans Autonomous Database à utiliser comme référentiel de métadonnées de Spatial Studio.

Durée estimée de l'atelier : 60 minutes

### A propos d'Oracle Spatial Studio

Oracle Spatial Studio (Spatial Studio) est une application Web qui fournit un accès en libre-service aux fonctionnalités spatiales d'Oracle Database. Bien que ces fonctionnalités aient toujours nécessité le codage et/ou l'utilisation d'outils 3e partie, Spatial Studio permet aux utilisateurs professionnels de créer et de partager des analyses spatiales et des cartes Web interactives à l'aide d'interfaces graphiques en libre-service.

![Texte de remplacement de l'image](./images/spatial-studio.png "Studio Spatial")

Spatial Studio utilise les données spatiales d'Oracle Database, c'est-à-dire les tables et les vues qui incluent le type de données de géométrie d'Oracle. Ces données sont des données spatiales préexistantes ou des données non spatiales préparées à l'aide de Spatial Studio pour ajouter des géométries basées sur des attributs.

Spatial Studio est une application Java EE qui peut être déployée vers Oracle Cloud à partir d'Oracle Cloud Marketplace. Spatial Studio peut également être déployé manuellement vers Oracle WebLogic ou Jetty, ou en tant que démarrage rapide prédéfini autonome à des fins de test.

Pour plus d'informations, veuillez visiter \[https://oracle.com/goto/spatialstudio\] (https://oracle.com/goto/spatialstudio)

### Objectifs

*   Apprendre à créer et affecter un schéma de base de données pour le référentiel de métadonnées de Spatial Studio
*   Découvrez comment utiliser Cloud Marketplace pour installer Spatial Studio
*   Découvrez comment désinstaller Spatial Studio lorsque cela n'est plus nécessaire

### Prérequis

*   Cet atelier nécessite Oracle Autonomous Database.
*   SQL Developer Web est fourni avec Autonomous Database. Il est également utilisé pour créer le schéma de référentiel Spatial Studio.
*   Si vous y avez déjà accès, après cette introduction, vous pouvez passer à l'exercice 3.
*   Sinon, passez à l'exercice 1.
*   Aucune expérience préalable d'Oracle Spatial n'est requise.
*   Compte Oracle Cloud - Consultez la page de destination LiveLabs de cet atelier pour connaître les environnements pris en charge

_Remarque : si vous disposez d'un compte **Essai gratuit**, à l'expiration de votre période d'évaluation gratuite, votre compte sera converti en compte **Toujours gratuit**. Vous ne pourrez pas organiser d'ateliers Free Tier à moins que l'environnement Always Free ne soit disponible. **[Cliquez ici pour accéder à la page FAQ sur le niveau gratuit.](https://www.oracle.com/cloud/free/faq.html)**_

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, Database Product Management, janvier 2021