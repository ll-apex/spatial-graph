# Intégrer l'analyse spatiale

## Présentation

Dans cet exercice, vous allez améliorer votre carte de l'exercice précédent en intégrant une analyse spatiale. Vous allez configurer une recherche d'aéroports situés à une distance définie par l'utilisateur d'un état sélectionné.

Temps de laboratoire estimé : 30 minutes

### Objectifs

*   Comprendre une opération d'analyse spatiale de base
*   Comprendre l'intégration de l'analyse spatiale dans la région de carte APEX

### Prérequis

*   Exercice 3 : Créer une carte à partir de zéro

## Tâche 1 : ajouter une région pour les filtres

1.  Cliquez sur **Page 3 : Carte des aéroports et des États** en haut de l'arborescence de gauche. Ensuite, dans le panneau des propriétés de page à droite, sous Apparence, remplacez le modèle de page par **Colonne gauche**.
    
    ![Mettre à jour le modèle de page](images/add-spatial-analysis-01a.png)
    
    Vous devez ensuite voir **LEFT COLUMN** dans la présentation.
    
    ![Mettre à jour le modèle de page](images/add-spatial-analysis-01b.png)
    
2.  Faites glisser une région Static Content vers la colonne de gauche.
    
    ![Ajouter une région de contenu statique](images/add-spatial-analysis-01c.png)
    
3.  Renommez la région **Mes filtres** ou le nom de votre choix.
    
    ![Renommer la région](images/add-spatial-analysis-02.png)
    

## Tâche 2 : ajouter un élément pour la sélection de l'état

1.  Faites glisser un élément de liste de sélection de votre région de filtres et mettez à jour le nom sur **P3\_STATE**.
    
    ![Ajouter un élément de liste de sélection](images/add-spatial-analysis-03.png)
    
2.  Dans les propriétés de l'élément de page à droite, faites défiler la page jusqu'à la section Liste de valeurs. Activez **Valeur requise** à l'aide du commutateur, définissez le type sur **Requête SQL** et entrez la requête suivante :
    
        <copy>
          select name, state_code
            from EBA_SAMPLE_MAP_SIMPLE_STATES
        order by name
        </copy>
        
    
    ![Requête SELECT](images/add-spatial-analysis-04.png)
    
3.  Dans les propriétés de l'élément de page à droite, faites défiler la page jusqu'à la section Default. Définissez le type sur **Statique** et la valeur sur **Texas** ou un autre état de votre choix (entre apostrophes).
    
    ![Configurer la liste de sélection](images/add-spatial-analysis-05.png)
    

## Tâche 3 : ajouter un élément pour la saisie de distance

1.  Faites glisser Number Field dans la région des filtres. Mettez à jour le nom sur **P3\_DISTANCE** et l'étiquette sur **Proximity (km)**.
    
    ![Ajouter un élément de champ numérique](images/add-spatial-analysis-06.png)
    
2.  Dans les propriétés de l'élément de page à droite, faites défiler la page jusqu'à la section Validation et activez **Valeur requise**.
    
    ![Définir la validation sur Valeur requise](images/add-spatial-analysis-07.png)
    
3.  Faites défiler la page jusqu'à la section Default. Définissez le type sur **Static** et la valeur sur **100**.
    
    ![Définir la valeur par défaut](images/add-spatial-analysis-08.png)
    
    Vous disposez maintenant d'entrées pour filtrer les aéroports en fonction de la proximité d'un état. Vous allez ensuite appliquer les filtres à l'aide d'actions dynamiques.
    

## Tâche 4 : Appliquer des filtres à l'aide d'actions dynamiques

Vous allez ensuite créer les actions appelées lorsque les valeurs d'état et/ou de distance sont modifiées par l'utilisateur.

1.  Cliquez avec le bouton droit de la souris sur l'élément P3\_STATE ou P3\_DISTANCE et sélectionnez **Créer une action dynamique** (l'action que nous créons sera appliquée aux deux éléments).
    
    ![Créer une action dynamique](images/add-spatial-analysis-09.png)
    
2.  Dans les propriétés Action dynamique de droite, définissez le nom sur **Valider et actualiser**. Sous la section Quand, définissez l'événement sur **Modifier**, le type de sélection sur **Articles** et les éléments sur la liste séparée par des virgules **P3\_DISTANCE,P3\_STATE**. Notez que le bouton situé à droite de la zone de texte des éléments vous permet de sélectionner des éléments dans une liste. Pour éviter de soumettre des valeurs négatives pour la distance, dans la section Condition côté client, définissez Type sur **Article >= Valeur**, Item sur **P3\_DISTANCE** et Value sur **0**.
    
    ![Configuration de l'action dynamique](images/add-spatial-analysis-10.png)
    
3.  Les actions dynamiques sont configurées avec des actions TRUE et FALSE appelées en fonction des conditions configurées. Dans ce cas, la condition côté client (P3\_DISTANCE >= 0) détermine s'il faut appeler l'action TRUE (la condition est satisfaite) ou l'action FALSE (la condition n'est pas satisfaite). Cela nous permettra de piéger l'entrée de distance négative.
    
    Lorsque la condition côté client est TRUE, l'action doit soumettre les valeurs d'entrée et actualiser la page. Cliquez sur l'action sous True. Dans les propriétés Action à droite, sous Identification, définissez l'action sur **Actualiser**. Sous Eléments affectés, définissez le type de sélection sur **Région** et la région sur **Ma région de carte** (ou le nom que vous avez utilisé si différent). Observez dans l'arborescence de la page de gauche que l'action Vrai passe à Rafraîchir.
    
    ![Configuration de l'action dynamique](images/add-spatial-analysis-11.png)
    
4.  Vous allez ensuite configurer l'action à appeler lorsque la condition côté client n'est pas remplie, ce qui signifie qu'une valeur de distance négative a été saisie. Sous Actions dynamiques pour l'un des éléments, cliquez avec le bouton droit de la souris sur Faux et sélectionnez **Créer une action FAUX**.
    
    ![Configuration de l'action dynamique](images/add-spatial-analysis-12.png)
    
5.  L'action FALSE appelée lorsque la distance est négative est un message contextuel destiné à l'utilisateur. Cliquez sur l'action False. Dans les propriétés Action à droite, sous Identification, définissez Action sur **Alert**. Sous Paramètres, définissez le titre sur **Distance non valide** (il s'agit de la bannière d'alerte) et le message sur **Distance doit être >= 0** (il s'agit du corps de l'alerte). Dans l'arborescence de la page de gauche, observez que l'action False passe à Alert.
    
    ![Configuration de l'action dynamique](images/add-spatial-analysis-13.png)
    
6.  Votre région de carte comprend actuellement une couche Etats affichant tous les états. Vous allez maintenant ajuster cette couche pour afficher uniquement l'état sélectionné dans le menu P3\_STATE. Dans l'arborescence de la page de gauche, sous Couches, cliquez sur Etats. Dans les propriétés de couche à droite, sous Identification, remplacez le nom par **Selected State**. Sous Source, définissez la clause Where sur **state\_code = :P3\_STATE**. Observez dans l'arborescence de la page de gauche que le nom de la couche passe à l'état sélectionné.
    
        <copy>
        state_code = :P3_STATE
        </copy>
        
    
    ![Configurer la clause WHERE](images/add-spatial-analysis-14.png)
    
7.  Enfin, vous mettez à jour la couche Aéroports pour renvoyer les éléments filtrés en fonction de l'état et de la proximité spécifiés par l'utilisateur. Dans l'arborescence Page à gauche, cliquez sur la couche Airports. Dans les propriétés de couche à droite, sous Source, remplacez Type par **Requête SQL**. Pour SQL Query, entrez l'instruction suivante qui utilise l'opérateur SQL natif "à distance" d'Oracle Database.
    
        <copy>
        select a.*
          from EBA_SAMPLE_MAP_AIRPORTS a,
               EBA_SAMPLE_MAP_SIMPLE_STATES b
         where b.state_code= :P3_STATE
           and a.land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance='|| :P3_DISTANCE ||' unit=KM') = 'TRUE'
        </copy>
        
    
    Pour les éléments de page à soumettre, entrez la liste séparée par des virgules **P3\_STATE,P3\_DISTANCE**.
    
    ![Requête SQL spatiale](images/add-spatial-analysis-15.png)
    
8.  Votre page est maintenant prête à être affichée. Cliquez sur **Enregistrer**, puis sur le bouton vert **Exécuter** en haut à droite. Une fois la page affichée, sélectionnez **Alabama** pour l'état. La carte affiche l'état sélectionné et les aéroports à moins de 100 km (la distance par défaut).
    
    ![Enregistrer et exécuter (page)](images/add-spatial-analysis-16.png)
    
9.  Définissez l'état sélectionné sur **Kansas**. Observez la carte affiche maintenant l'état sélectionné et les aéroports avec 100 km.
    
    ![Sélectionner Kansas](images/add-spatial-analysis-17.png)
    
10.  Augmentez la distance à 600 km, puis cliquez sur Entrée ou Tab pour soumettre. Observez que la carte affiche maintenant des aéroports supplémentaires dans la plus grande distance.
    
    ![Augmenter la distance à 600 km](images/add-spatial-analysis-18.png)
    
11.  Enfin, confirmez que la soumission d'une distance négative entraîne la fenêtre contextuelle Erreur que nous avons configurée précédemment.
    
    ![Alerte de distance négative](images/add-spatial-analysis-19.png)
    
    Comme le montre l'application Sample Maps que vous avez installée au début de cet atelier, il y a une énorme quantité de fonctionnalités supplémentaires qui peuvent être réalisées avec Map Regions et Spatial. Cet atelier a présenté les bases et nous espérons que votre intérêt a été suscité et que vous tirerez parti de la puissance des cartes et des analyses spatiales dans vos applications APEX.
    

## En savoir plus

*   [Oracle Spatial](https://www.oracle.com/database/spatial/)
*   [APEX](https://apex.oracle.com/)

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, Database Product Management, mars 2023