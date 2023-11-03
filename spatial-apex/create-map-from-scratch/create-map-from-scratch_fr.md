# Créer une carte entièrement nouvelle

## Présentation

Dans cet exercice, vous allez créer une page dans votre application, puis configurer une région Map Region à partir de zéro.

Temps de laboratoire estimé : 15 minutes

### Objectifs

*   Comprendre la configuration de la région de carte APEX

### Prérequis

*   Exercice 2 : Créer une carte à l'aide d'un assistant

## Tâche 1 : créer une page

1.  Dans le chemin de navigation en haut à gauche, cliquez sur le lien correspondant au répertoire de base de votre application. Cliquez ensuite sur l'onglet **Disposition**. ![Présentation de page](images/create-map-15a.png)
    
2.  Cliquez sur **Créer une page**. ![Assistant Créer une page](images/create-map-15b.png)
    
3.  Vous pouvez sélectionner Map ici pour avoir le même assistant que celui que vous avez vu dans l'assistant Créer une application. Mais cette étape consiste à créer une carte à partir de zéro, par exemple si vous aviez une page existante. Sélectionnez **Page vide**, puis cliquez sur **Suivant**. ![Sélectionner une page vierge](images/create-map-16.png)
    
4.  Pour le nom, entrez **Carte des aéroports et des États**, puis cliquez sur **Suivant**. ![Nom de la page](images/create-map-16a.png)
    
5.  Sélectionnez l'option permettant de créer une nouvelle entrée de menu de navigation et entrez **Carte des aéroports et des États**, c'est-à-dire identique au nom de la page. Cliquez ensuite sur **Suivant**. ![Créer une entrée de menu de navigation](images/create-map-17.png)
    
6.  Consultez le récapitulatif et cliquez sur **Terminer**. ![Récapitulatif à vérifier](images/create-map-18.png)
    

## Tâche 2 : ajouter une carte à la page

1.  Faites glisser **Mapper** de la palette Régions en bas et déposez-le sous la section Corps de la mise en page. Observez que la région Map apparaît dans l'arborescence Page sous Body avec le nom par défaut New. Cliquez sur **Nouveau** dans l'arborescence de la page et observez ses propriétés à droite. Notez que le type de région est Map. ![Ajouter une région de carte](images/create-map-19.png)
    
2.  Dans le panneau de droite, remplacez le titre de région Nouveau par le nom de votre choix, par exemple **Région Ma carte**. Notez que le titre est mis à jour dans l'arborescence de la page de gauche. ![Saisir le titre de la région](images/create-map-20.png)
    
3.  Notez que Map Region inclut un élément enfant nommé Layers avec une couche par défaut nommée New. Les couches sont le contenu orienté données à afficher sur la carte. Cliquez sur la couche **Nouveau** dans l'arborescence de la page pour afficher ses propriétés dans le panneau de droite. ![Afficher les propriétés de la couche](images/create-map-21.png)
    
4.  Mettez à jour le nom de couche sur **Airports** et le type sur **Points**. Observez la mise à jour du nom de couche dans l'arborescence de page sur la gauche. ![Mettre à jour les propriétés de la couche](images/create-map-23.png)
    
5.  Faites défiler l'affichage vers le bas dans le panneau des propriétés de couche situé à droite. Mettez à jour la **source** pour utiliser la table **EBA\_SAMPLE\_MAP\_AIRPORTS**. Pour limiter l'affichage des aéroports dans la couche, ajoutez la clause WHERE **LAND\_AREA\_COVERED > 2500**. Activez l'option Utiliser l'index spatial à l'aide du commutateur. ![Mettre à jour les propriétés de la couche](images/create-map-24.png)
    
6.  Faites défiler l'affichage vers le bas dans le panneau des propriétés de couche, à droite, jusqu'à la section **Mappage de colonnes**. C'est là que vous configurez la colonne spatiale pour le rendu. Sélectionnez le type de données de géométrie **SDO\_GEOMETRY** et la colonne de géométrie **GEOMETRY**. ![Mettre à jour les propriétés de la couche](images/create-map-25.png)
    
7.  Faites défiler l'affichage vers le bas dans le panneau des propriétés de couche, à droite, jusqu'à la section **Fenêtre d'informations**. C'est là que vous pouvez configurer le contenu d'une fenêtre d'informations qui apparaît lorsque vous cliquez sur un élément de la carte. Activez le **formatage avancé** en cliquant sur le bouton de permutation, puis collez les éléments suivants dans la zone de texte **Expression HTML** :
    
        <copy>
        <strong>&AIRPORT_NAME.</strong><br>
        &CITY., &STATE_NAME.<br>
        Code: &IATA_CODE.
        </copy>
        
    
    ![Mettre à jour les propriétés de la couche](images/create-map-25a.png)
    

## Tâche 3 : ajouter une couche à la carte

1.  Dans l'arborescence de page de gauche, cliquez avec le bouton droit de la souris sur **Couches** sous votre région de carte et sélectionnez **Créer une couche**. ![Ajouter une couche](images/create-map-26.png)
    
2.  Cliquez sur la couche que vous venez de créer dans l'arborescence Page sous Map Region. Ensuite, dans le panneau Détails de la couche à droite, mettez à jour le nom sur **Etats**, le type de couche sur **Polygones** et la source sur **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES**. ![Mettre à jour les propriétés de la couche](images/create-map-27.png)
    
3.  Les couches sont affichées dans l'ordre dans lequel elles apparaissent sous Couches dans l'arborescence de la page. Pour que les aéroports s'affichent dans les états supérieurs, faites glisser la couche **Etats** au-dessus de la couche Aéroports sous Couches dans l'arborescence de la page. Faites défiler l'affichage vers le bas dans le panneau de détails de la couche, à droite, jusqu'à la section Mapping de colonne. Sélectionnez le type de données de géométrie **SDO\_GEOMETRY** et la colonne de géométrie **GEOMETRY**. Sous Apparence, sélectionnez les couleurs de remplissage et de contour de votre choix. Définissez l'opacité de remplissage sur une valeur de votre choix, en notant qu'une valeur de 1 signifie totalement opaque afin que la carte d'arrière-plan ne soit pas visible. ![Mettre à jour l'ordre des couches](images/create-map-28.png)
    
4.  En haut à droite, cliquez sur **Enregistrer**, puis sur le bouton vert **Exécuter**. ![Enregistrer et exécuter (page)](images/create-map-29.png)
    
5.  Observez le rendu de votre carte avec les couches States et Airports. Cliquez et faites glisser la carte pour effectuer un panoramique, puis utilisez le contrôle de navigation en haut à droite pour effectuer un zoom avant ou arrière. Cliquez sur un aéroport pour voir la fenêtre d'informations que vous avez configurée. Passez la souris sur un état pour afficher l'info-bulle que vous avez configurée. Désactivez et activez les calques avec les cases à cocher sous la carte. ![Interagir avec la carte](images/create-map-30.png)
    

Félicitations pour la création de votre première carte à partir de zéro. Dans le prochain laboratoire, vous incorporerez l'analyse spatiale dans cette carte.

Ceci conclut le laboratoire. Vous pouvez maintenant passer à l'exercice suivant.

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, Database Product Management, mars 2023