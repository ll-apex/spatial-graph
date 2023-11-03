# Créer des exemples de données

## Présentation

Cet atelier vous guide tout au long des étapes de création d'exemples de données spatiales dans Oracle Database.

Temps de laboratoire estimé : 10 minutes

### Objectifs

Dans cet exercice, vous allez :

*   En savoir plus sur la gestion des données spatiales dans Oracle Database
*   Préparer des données spatiales dans Oracle Database à partir de formats de fichier courants

### Prérequis

*   Achèvement du laboratoire 2

### A propos des données spatiales

Oracle Database stocke les données spatiales (points, lignes, polygones) dans un type de données natif appelé SDO\_GEOMETRY. Oracle Database fournit également un index spatial natif pour les opérations spatiales hautes performances. Cet index spatial repose sur les métadonnées spatiales saisies pour chaque table et colonne de géométrie stockant des données spatiales. Une fois les données spatiales remplies et indexées, des API robustes sont disponibles pour effectuer des analyses, des calculs et des traitements spatiaux.

Le type SDO\_GEOMETRY a le format général suivant :

    SDO_GEOMETRY( 
     [geometry type],           --ID for point/line/polygon
     [coordinate system],       --ID of coordinate system
     [point coordinate],        --for points only
     [line/polygon info],       --for lines/polygons only
     [line/polygon coordinates] --for lines/polygons only
      )
    

Les types de géométrie les plus courants sont 2 dimensions :

| ID | Type |
| --- | --- |
| 2001 | Point |
| 2002 | Ligne |
| 2003 | Polygone |

Les systèmes de coordonnées les plus courants sont les suivants :

| ID | Système de coordonnées |
| --- | --- |
| (4326) | Latitude/longitude |
| (3857) | Mercure du Monde |

Lorsque vous utilisez la latitude/longitude, notez que la latitude est la coordonnée Y et que la longitude est la coordonnée X. Comme les coordonnées sont répertoriées en tant que paire X, Y, les valeurs sont en fait dans l'ordre longitude, latitude.

Voici un exemple de géométrie de point utilisant des coordonnées de latitude/longitude :

    SDO_GEOMETRY( 
     2001,               --2D point
     4326,               --latitude/longitude
     SDO_POINT_TYPE(     
        -100.123, 20.456 --coordinate
        ),         
     NULL,               --for lines/polygons only
     NULL                --for lines/polygons only
      )
    

Voici un exemple de géométrie de polygone utilisant des coordonnées de latitude/longitude :

    SDO_GEOMETRY( 
     2003,                  --2D polygon
     4326,                  --latitude/longitude
     NULL,                  --for points only       
     SDO_ELEM_INFO_ARRAY(
          1, 1003, 1        --indicates simple exterior polygon
            ), 
     SDO_ORDINATE_ARRAY(   
        -98.789065,39.90973, -- coordinates
        -101.2522,39.639537,
        -99.84374,37.160316,
        -96.67987,35.460699,
        -94.21875,39.639537,
        -98.789025,39.90973
          )
        )
    );
    

### Objectifs

Dans cet exercice, vous allez :

*   Créer des tables avec une colonne de géométrie
*   Alimenter les géométries
*   Créer des métadonnées et des index spatiaux

### Prérequis

Comme décrit dans l'introduction de l'atelier, vous devez accéder à Oracle Database et SQL Client. Si vous ne disposez pas de ces éléments, revenez aux sections sur le compte Oracle Cloud, Autonomous Database et SQL Developer Web.

## Tâche 1 : créer des tables avec des coordonnées

Nous commençons par créer des tables avec des coordonnées de latitude et de longitude. Il s'agit d'un point de départ commun pour créer des données spatiales, par exemple des coordonnées à partir du GPS, ou à partir d'une adresse postale ou d'une adresse IP géocodée.

Les instructions et les captures d'écran font référence à SQL Developer Web. Toutefois, les mêmes étapes s'appliquent aux autres clients SQL.

1.  Téléchargez le script SQL [ici](files/create-sample-data.sql).
    
2.  Copier/coller/exécuter le script dans SQL Developer Web ![Texte de remplacement de l'image](images/run-script-1.png)
    
3.  Actualiser la liste pour voir les tableaux BRANCHES et WAREHOUSES
    
    ![Texte de remplacement de l'image](images/refresh-tables-1.png)
    

## Tâche 2 : créer des géométries à partir de coordonnées

Les géométries peuvent être alimentées par SQL, pour la casse exathis, en spécifiant les coordonnées des géométries de points en fonction des colonnes de latitude et de longitude.

1.  Ajoutez des colonnes de géométrie :
    
        <copy> 
        ALTER TABLE WAREHOUSES ADD (
         GEOMETRY SDO_GEOMETRY
        );
        
        ALTER TABLE BRANCHES ADD (
           GEOMETRY SDO_GEOMETRY
        );
        </copy>
        
2.  Remplir les colonnes de géométrie :
    
        <copy> 
        UPDATE WAREHOUSES
        SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
         UPDATE BRANCHES
         SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
        </copy>
        

## Tâche 3 : créer une table avec un polygone

Les lignes et les polygones peuvent être créés de la même manière. Alors qu'une géométrie ponctuelle nécessite une coordonnée, les lignes et les polygones nécessitent toutes les coordonnées qui définissent la géométrie. Dans ce cas, nous créons une table pour stocker un polygone.

1.  Créer une table et insérer une ligne
    
        <copy>
        CREATE TABLE COASTAL_ZONE (
            ZONE_ID   NUMBER,
            GEOMETRY  SDO_GEOMETRY
        );       
        
        INSERT INTO COASTAL_ZONE VALUES (
            1,
            SDO_GEOMETRY(
                2003, 4326, NULL, SDO_ELEM_INFO_ARRAY(
                    1, 1003, 1
                ), SDO_ORDINATE_ARRAY(
                    -93.719934, 30.210638,
                    -95.422592, 29.773714, 
                    -95.059698, 29.322204, 
                    -96.013892, 28.787021, 
                    -96.660964, 28.925638, 
                    -97.528688, 28.042050, 
                    -97.858501, 27.447461, 
                    -97.497364, 25.880056, 
                    -96.977826, 25.969716, 
                    -97.211445, 27.054605, 
                    -96.870226, 27.816077, 
                    -93.794290, 29.535729, 
                    -93.719934, 30.210638
                )
            )
        );
        </copy>
        
2.  Actualisez la liste des tables pour afficher la table COASTAL\_ZONE. ![Texte de remplacement de l'image](images/refresh-tables-2.png)
    

## Tâche 4 : ajouter des métadonnées et des index spatiaux

Oracle Database fournit un index spatial natif pour les opérations spatiales hautes performances. Nos données d'échantillon sont si petites qu'un index spatial n'est pas vraiment nécessaire. Toutefois, nous procédons comme suit, car elles sont importantes pour les volumes de données de production standard. Un index spatial nécessite une ligne de métadonnées pour la géométrie indexée. Nous créons ces métadonnées, puis les index spatiaux.

1.  Ajoutez des métadonnées spatiales :
    
        <copy> 
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'WAREHOUSES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'BRANCHES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'COASTAL_ZONE',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        </copy>
        
2.  Créer des index spatiaux :
    
        <copy> 
        CREATE INDEX WAREHOUSES_SIDX ON
            WAREHOUSES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX BRANCHES_SIDX ON
            BRANCHES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX COASTAL_ZONE_SIDX ON
            COASTAL_ZONE (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
         </copy>
        
    
    Une fois les index créés, actualisez la liste des tables. 3 tables dont le nom commence par MDRT\_ apparaissent. Il s'agit d'artefacts des index spatiaux gérés automatiquement par Oracle Database. Vous ne devez jamais manipuler manuellement ces tables. ![Texte de remplacement de l'image](images/refresh-tables-3.png)
    
    Nos données échantillon sont maintenant préparées et prêtes pour les requêtes spatiales.
    
    Vous pouvez maintenant passer à l'exercice suivant.
    
    Si vous devez rétablir cet exercice et supprimer les éléments créés, exécutez la commande suivante :
    
         DROP TABLE BRANCHES;   
         DROP TABLE WAREHOUSES;
         DROP TABLE COASTAL_ZONE;
         DELETE FROM USER_SDO_GEOM_METADATA;
         COMMIT;
        

## En savoir plus

*   \[Portail de produits spatiaux\] (https://oracle.com/goto/spatial)
*   [Documentation spatiale](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Blogs spatiaux](https://blogs.oracle.com/oraclespatial/)

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - Kamryn Vinson, novembre 2020