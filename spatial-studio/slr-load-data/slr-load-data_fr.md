# Charger et préparer les données

## Présentation

Spatial Studio fonctionne sur des données stockées dans des bases de données Oracle. Dans Spatial Studio, vous utilisez des jeux de données, qui sont des tables et des vues de base de données accessibles via des connexions de base de données. Les jeux de données sont des pointeurs vers des tables et des vues de base de données. Ils peuvent avoir des noms conviviaux plus autodescriptifs que le nom de la table ou de la vue de base de données sous-jacente.

Les utilisateurs ont souvent besoin d'incorporer des données acquises à partir de différentes sources. Pour ce faire, Spatial Studio fournit des fonctionnalités permettant de charger des données dans Oracle Database à partir de formats standard. Cela inclut le chargement des 2 formats les plus courants pour l'échange de données spatiales : les fichiers Shapefiles et les fichiers GeoJSON. En plus du chargement des formats spatiaux, Spatial Studio prend en charge le chargement des feuilles de calcul et des fichiers CSV. Dans ce cas, une préparation supplémentaire est nécessaire pour dériver des géométries à partir d'attributs spatiaux tels que les adresses ("géocodage d'adresse") et les coordonnées latitude/longitude ("indexation de coordonnées"). Cet atelier vous explique comment charger et préparer des données dans ces formats à l'aide de Spatial Studio.

**Veuillez noter les informations importantes suivantes sur les données publiques utilisées dans cet atelier :**

Dans cet exercice, vous allez télécharger un seul fichier ZIP contenant les éléments suivants :

*   **Régions inondables prévues** simplifiées à partir des données publiques publiées sur [https://data.boston.gov/group/geospatial?q=sea+level+rise+flood](https://data.boston.gov/group/geospatial?q=sea+level+rise+flood). Étant donné qu'ils ont été simplifiés à partir de leur forme publiée, ils ne sont pas destinés à représenter l'étendue précise des modèles publiés.
*   **Bâtiments** extraits des données publiques publiées sur [https://www.mass.gov/info-details/massgis-data-building-structures-2-d](https://www.mass.gov/info-details/massgis-data-building-structures-2-d).
*   **Schools** à partir de OpenStreetMap extrait à l'aide de [https://wiki.openstreetmap.org/wiki/Overpass\_turbo](https://wiki.openstreetmap.org/wiki/Overpass_turbo)
*   **Installations TRI** de l'EPA des Etats-Unis extraites à l'aide de [https://edap.epa.gov/public/extensions/TRIToxicsTracker/TRIToxicsTracker.html](https://edap.epa.gov/public/extensions/TRIToxicsTracker/TRIToxicsTracker.html). Le Toxics Release Inventory (TRI) est une ressource pour se renseigner sur les rejets chimiques toxiques et les activités de prévention de la pollution signalées par les installations industrielles et fédérales.

Temps de laboratoire estimé : 10 minutes

Regardez la vidéo ci-dessous pour une présentation rapide du laboratoire.

[Charger et préparer les données](videohub:1_h1cmu08i)

### Objectifs

*   Apprendre à charger et préparer des données spatiales

### Prérequis

*   Atelier complet 1 : Déployer Spatial Studio sur Oracle Cloud
*   Aucune expérience préalable d'Oracle Spatial n'est requise.

## Tâche 1 : Charger des données

Vous commencez par charger les régions inondables projetées, les parcelles, les écoles et les installations à partir de formats communs.

1.  Téléchargez le fichier ZIP contenant les données à un emplacement pratique : [SpatialStudioSlrData.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/jyHA4nclWcTaekNIdpKPq3u2gsLb00v_1mmRKDIuOEsp--D6GJWS_tMrqGmb85R2/n/c4u04/b/livelabsfiles/o/labfiles/SpatialStudioSlrData.zip). Le fichier ZIP contient les éléments suivants :
    
    ![Télécharger et vérifier les données échantillon](images/load-data-01.png)
    
2.  Dans Spatial Studio, dans le menu du panneau de gauche, accédez à la page Ensembles de données, cliquez sur **Créer un ensemble de données** et sélectionnez **A partir du téléchargement de fichier**. Cliquez sur la région de téléchargement, accédez à votre emplacement de téléchargement et sélectionnez le fichier ZIP. Vous pouvez également faire glisser le fichier vers la région de téléchargement. Cliquez ensuite sur **Créer**.
    
    ![Charger des données dans Spatial Studio pour créer des ensembles de données](images/load-data-02.png)
    
3.  Un aperçu du 1er fichier chargé sera affiché. Sélectionnez la connexion de destination pour ce téléchargement. Sélectionnez la connexion **SPATIAL\_STUDIO** (référentiel de métadonnées Spatial Studio). Dans un scénario de production, vous auriez d'autres connexions pour ces données métier, distinctes du référentiel de métadonnées. Cliquez sur **Soumettre** pour lancer le 1er chargement.
    
    ![Boîte de dialogue Créer un ensemble de données](images/load-data-03.png)
    
4.  Répétez cette opération pour tous les ensembles de données.
    
5.  Lorsque vous avez terminé, les jeux de données sont répertoriés avec une petite icône d'avertissement pour indiquer que 1 ou plusieurs étapes de préparation sont nécessaires. Vous allez effectuer ces étapes dans la tâche suivante.
    
    ![Charger des données](images/load-data-04.png)
    

## Tâche 2 : Préparer les données

La préparation des données comprend des opérations qui permettent d'utiliser des ensembles de données pour l'analyse spatiale et la visualisation de cartes. Exemples : géocodage d'adresse, indexation de coordonnées et identification de colonnes de clé uniques. Dans cette tâche, vous effectuez l'indexation des coordonnées et définissez des clés de jeu de données.

1.  Les jeux de données sont répertoriés avec une petite icône d'avertissement pour indiquer que 1 ou plusieurs étapes de préparation sont nécessaires. Commencez par cliquer sur le badge d'avertissement pour **SCHOOLS**. Ce jeu de données a été chargé à partir d'un format non spatial (csv) et nécessite une préparation pour la visualisation de mapping. L'ensemble de données inclut des colonnes de latitude/longitude. Sélectionnez **Créer un index de latitude/longitude**, puis cliquez sur **OK**.
    
    ![Correction d'un problème avec un index lon/lat manquant](images/prep-data-01.png)
    
2.  Renseignez les colonnes de latitude et de longitude pour l'indexation, puis cliquez sur **OK**.
    
    ![Mapper les colonnes de longitude et de latitude](images/prep-data-02.png)
    
3.  Répétez l'opération pour **FACILITIES** en cliquant sur le badge d'avertissement et en sélectionnant **Créer un index de latitude/longitude**. Lorsque vous avez terminé, notez que les icônes SCHOOLS et FACILITIES sont passées d'un tableau à une broche indiquant que les jeux de données peuvent être utilisés pour la visualisation de carte.
    
4.  Les autres badges d'avertissement indiquent que des clés doivent être définies pour vos jeux de données. Bien qu'elles ne soient pas requises pour la mise en correspondance de base, ajoutez des clés car elles sont requises pour les analyses que vous effectuerez plus tard dans l'atelier. Cliquez sur l'icône d'avertissement **BUILDINGS**. Cliquez sur le lien **Accéder aux colonnes de jeu de données**.
    
    ![Créer une colonne de clé](images/prep-data-bldgs-00.png)
    
    Cliquez sur le bouton **Créer une colonne de clé**.  
    ![Créer une colonne de clé](images/prep-data-bldgs-01.png)
    
    Nommez la colonne de clé **bldg\_id** et cliquez sur **OK**.  
    ![Nommer la colonne de clé](images/prep-data-bldgs-02.png)
    
    Enfin, cliquez sur **Appliquer**. ![Indiquer la colonne de clé pour le jeu de données](images/prep-data-bldgs-03.png)
    
5.  Cliquez sur l'icône d'avertissement **FACILITIES** et cliquez sur le lien **Accéder aux colonnes de jeu de données**.
    
    ![Correction d'un problème avec une colonne de clé manquante](images/prep-data-03.png)
    
6.  Sélectionnez **FACILITY\_ID** comme clé, cliquez sur **Valider la clé**, puis sur **Appliquer**.
    
    ![Rechercher une colonne de clé dans les propriétés de jeu de données](images/prep-data-04.png)
    
7.  Répétez cette opération pour ajouter des clés pour vos autres jeux de données à l'aide des colonnes suivantes :
    
    | Ensemble de données | Colonne à utiliser comme clé |
    | --- | --- |
    | FLOOD2040 | ID de famille |
    | FLOOD2060 | ID de famille |
    | FLOOD2080 | ID de famille |
    | ECOLES | OGR\_FID |
    
8.  Notez que tous vos ensembles de données sont entièrement préparés pour la cartographie et l'analyse spatiale.
    
    ![Charger des données](images/prep-data-05.png)
    

Vous pouvez maintenant **passer à l'exercice suivant**.

## En savoir plus

*   [Page produit Oracle Spatial](https://www.oracle.com/database/spatial)
*   [Lancez-vous avec Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)
*   [Documentation de Spatial Studio](https://docs.oracle.com/en/database/oracle/spatial-studio)

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Contributeurs** - Jayant Sharma, Denise Myrick
*   **Dernière mise à jour par/date** - David Lapp, août 2023