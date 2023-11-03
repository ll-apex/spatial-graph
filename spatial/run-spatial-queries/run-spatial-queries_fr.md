# Requêtes spatiales

## Présentation

Cet atelier vous guide tout au long des requêtes spatiales de base dans Oracle Database. Vous utiliserez les exemples de données créés au cours de l'exercice précédent pour identifier les éléments en fonction de leur proximité et de leur confinement.

Temps de laboratoire estimé : 15 minutes

### A propos des requêtes spatiales

Oracle Database inclut une bibliothèque robuste de fonctions et d'opérateurs pour l'analyse spatiale. Cela inclut les relations spatiales, les mesures, les agrégations, les transformations et bien plus encore. Ces opérations sont accessibles via SQL natif, PL/SQL, les API Java et tout autre langage qui communique avec Oracle Database.

### Objectifs

Dans cet exercice, vous allez :

*   Identifier les MARQUES ayant des relations de proximité avec un ENTREPÔT
*   Identifier les MARQUES ayant des relations de confinement et de proximité avec un COASTAL\_ZONE

### Prérequis

*   Fin de l'exercice précédent ; création d'exemples de données spatiales

## Requêtes spatiales

Les requêtes spatiales dans Oracle Database sont comme toutes les autres requêtes traditionnelles auxquelles vous êtes habitué. La seule différence est un ensemble de fonctions spatiales et d'opérateurs qui sont probablement nouveaux pour vous.

**Identifiez 5 succursales les plus proches de l'entrepôt de Dallas :**

    <copy> 
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5'
        ) = 'TRUE';
    </copy>
    

![Exécuter une requête spatiale](images/query1.png) Remarques :

*   L'opérateur `SDO_NN` renvoie les n branches les plus proches à Dallas Warehouse, où 'n' est la valeur spécifique de `SDO_NUM_RES`. Le premier argument de `SDO_NN` (`B.GEOMETRY` dans l'exemple ci-dessus) est la colonne à rechercher. Le deuxième argument (`W.GEOMETRY` dans l'exemple ci-dessus) est l'emplacement auquel vous souhaitez rechercher les voisins les plus proches. Aucune hypothèse ne doit être faite sur l'ordre des résultats renvoyés. Par exemple, il n'est pas garanti que la première ligne renvoyée soit la plus proche. Si deux branches ou plus sont à distance égale de l'entrepôt, l'une ou l'autre peut être renvoyée lors des appels suivants à `SDO_NN`.
*   Lors de l'utilisation du paramètre `SDO_NUM_RES`, aucun autre critère n'est utilisé dans la clause `WHERE`. `SDO_NUM_RES` prend uniquement en compte la proximité. Par exemple, si vous avez ajouté un critère à la clause `WHERE` car vous voulez que les cinq branches les plus proches aient un code postal spécifique et que quatre des cinq branches les plus proches aient un code postal différent, la requête ci-dessus renvoie une ligne. Ce comportement est spécifique au paramètre `SDO_NUM_RES`. Dans une requête ci-dessous, vous utiliserez un autre paramètre pour le scénario de critères de requête supplémentaires.

**Identifiez 5 succursales les plus proches de l'entrepôt de Dallas avec la distance :**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5 unit=km', 1
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Exécuter une requête spatiale](images/query2.png) Remarques :

*   L'opérateur `SDO_NN_DISTANCE` est un opérateur auxiliaire de l'opérateur `SDO_NN` ; il ne peut être utilisé que dans l'opérateur `SDO_NN`. L'argument pour cet opérateur est un nombre qui correspond au nombre spécifié comme dernier argument de `SDO_NN` ; dans cet exemple, il s'agit de 1. Il n'y a pas de sens caché à cet argument, c'est simplement une étiquette. Si `SDO_NN_DISTANCE()` est spécifié, vous pouvez trier les résultats par distance et garantir que la première ligne renvoyée est la plus proche. Si les données que vous interrogez sont stockées sous forme de longitude et de latitude, l'unité par défaut pour `SDO_NN_DISTANCE` est les compteurs.
*   L'opérateur `SDO_NN` comporte également un paramètre `UNIT` qui détermine l'unité de mesure renvoyée par `SDO_NN_DISTANCE`.
*   La clause `ORDER BY DISTANCE` garantit que les distances sont renvoyées dans l'ordre, avec la distance la plus courte en premier.

**Identifiez les 5 succursales les plus proches de l'entrepôt de Dallas avec la distance :**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND B.BRANCH_TYPE = 'WHOLESALE'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_batch_size=5 unit=km', 1
        ) = 'TRUE'
        AND ROWNUM <= 5
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Exécuter une requête spatiale](images/query3.png) Remarques :

*   `SDO_BATCH_SIZE` est un paramètre réglable qui peut affecter les performances de votre requête. `SDO_NN` calcule en interne ce nombre de distances à la fois. Le lot initial de lignes renvoyées peut ne pas respecter les contraintes de la clause WHERE. Le nombre de lignes spécifié par `SDO_BATCH_SIZE` est donc renvoyé en continu jusqu'à ce que toutes les contraintes de la clause WHERE soient satisfaites. Vous devez choisir un élément `SDO_BATCH_SIZE` qui renvoie initialement le nombre de lignes susceptibles de satisfaire les contraintes de votre clause WHERE.
*   Le paramètre `UNIT` utilisé dans l'opérateur `SDO_NN` indique l'unité de mesure du paramètre `SDO_NN_DISTANCE`. L'unité par défaut est l'unité de mesure associée aux données. Pour les données de longitude et de latitude, la valeur par défaut est mètres.
*   `B.BRANCH_TYPE = 'WHOLESALE' AND ROWNUM <= 5` sont les contraintes supplémentaires dans la clause `WHERE`. La clause rownum est nécessaire pour limiter le nombre de résultats renvoyés à 5.
*   La clause `ORDER BY DISTANCE_KM` garantit que les distances sont renvoyées dans l'ordre, avec la distance la plus courte en premier et les distances mesurées en miles.

**Identifier les succursales à moins de 50 km de Houston Warehouse :**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE';
    </copy>
    

![Exécuter une requête spatiale](images/query4.png) Remarques :

*   Le premier argument de `SDO_WITHIN_DISTANCE` est la colonne à rechercher. Le deuxième argument est l'emplacement à partir duquel vous voulez déterminer les distances. Aucune hypothèse ne doit être faite sur l'ordre des résultats renvoyés. Par exemple, la première ligne renvoyée n'est pas garantie comme étant le client le plus proche de l'entrepôt 3.
*   Le paramètre DISTANCE utilisé dans l'opérateur `SDO_WITHIN_DISTANCE` indique la valeur de distance ; dans cet exemple, il s'agit de 100.
*   Le paramètre UNIT utilisé dans l'opérateur `SDO_WITHIN_DISTANCE` indique l'unité de mesure du paramètre DISTANCE. L'unité par défaut est l'unité de mesure associée aux données. Pour les données de longitude et de latitude, la valeur par défaut est mètres ; dans cet exemple, il s'agit de miles.

**Identifier les succursales à moins de 50 km de Houston Warehouse avec la distance :**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE,
        ROUND(
            SDO_GEOM.SDO_DISTANCE(
                B.GEOMETRY, W.GEOMETRY, 0.05, 'unit=km'
            ), 2
        ) AS DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Exécuter une requête spatiale](images/query5.png) Remarques :

*   La fonction `SDO_GEOM.SDO_DISTANCE` calcule la distance entre les succursales et l'entrepôt de Houston.
*   Les 2 premiers arguments de `SDO_GEOM.SDO_DISTANCE` sont les emplacements BRANCH et WAREHOUSE pour le calcul de distance.
*   Le troisième argument de `SDO_GEOM.SDO_DISTANCE` est la valeur de tolérance. La tolérance est une valeur d'erreur d'arrondi utilisée par Oracle Spatial. La tolérance est exprimée en mètres pour les données de longitude et de latitude. Dans cet example, la tolérance est de 50 mm.
*   Le paramètre UNIT utilisé dans le paramètre `SDO_GEOM.SDO_DISTANCE` indique l'unité de mesure de la distance calculée par la fonction `SDO_GEOM`.`SDO_DISTANCE`. L'unité par défaut est l'unité de mesure associée aux données. Pour les données de longitude et de latitude, la valeur par défaut est mètres. Dans cet exemple, il s'agit de miles.
*   La clause `ORDER BY DISTANCE_IN_MILES` garantit que les distances sont renvoyées dans l'ordre, avec la distance la plus courte en premier et les distances mesurées en miles.

**Identifier les branches dans la zone côtière :**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE';
    </copy>
    

![Exécuter une requête spatiale](images/query6.png) Remarques :

*   L'opérateur `SDO_ANYINTERACT` accepte 2 arguments, geometry1 et geometry2. L'opérateur renvoie `TRUE` pour les lignes où geometry1 se trouve à l'intérieur ou aux limites de geometry2.
*   Dans cet exemple, geometry1 correspond à `B.GEOMETRY`, les géométries de branche et geometry2 à `C.GEOMETRY`, la géométrie de zone côtière. La table COASTAL\_ZONE ne comporte que 1 ligne. Aucun critère supplémentaire n'est donc nécessaire.

**Identifier les branches à l'extérieur et à moins de 10 km de la zone côtière :**

    <copy>
    
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_WITHIN_DISTANCE(
            B.GEOMETRY, C.GEOMETRY, 'distance=10 unit=km'
        ) = 'TRUE'
    )
    MINUS
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE'
    );
    </copy>
    

![Exécuter une requête spatiale](images/query7.png) Remarques :

*   Dans la première partie de cette requête, l'opérateur `SDO_WITHIN_DISTANCE` identifie BRANCHES à moins de 10 km de COASTAL\_ZONE. Cela inclut les marques dans le COASTAL\_ZONE.
*   La requête utilise `MINUS` pour enlever BRANCHES dans COASTAL\_ZONE, ne laissant que BRACNCHES dans un rayon de 10 km et en dehors de COASTAL\_ZONE.

## En savoir plus

*   \[Portail de produits spatiaux\] (https://oracle.com/goto/spatial)
*   [Documention spatiale](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Blogs spatiaux](https://blogs.oracle.com/oraclespatial/)

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - Kamryn Vinson, novembre 2020