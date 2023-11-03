# Créer une carte avec l'assistant

## Présentation

Oracle APEX fournit un assistant permettant de créer divers types de page utiles. Dans cet exercice, vous allez utiliser l'assistant pour créer une application et une page avec une carte. Vous examinez ensuite la page obtenue pour comprendre la région Map.

Temps de laboratoire estimé : 10 minutes

### Objectifs

*   Comprendre les bases de la région de carte APEX

### Prérequis

*   Fin de l'exercice 1 : Installer l'application Sample Maps

## Tâche 1 : créer une application avec une page de carte à l'aide de l'assistant

L'assistant permet de créer rapidement et facilement une nouvelle application et votre première carte.

1.  Accédez à **App Builder** et cliquez sur **Créer**. ![Assistant Créer une application dans App Builder](images/create-map-01.png)
    
2.  Sélectionnez **Nouvelle application**. ![Créer une application - Nouvelle application](images/create-map-02.png)
    
3.  Entrez le nom de l'application et cliquez sur **Ajouter une page**. ![Créer une demande - Formulaire](images/create-map-03.png)
    
4.  Sélectionnez **Mapper** comme type de page. ![Créer une application - Ajouter une page](images/create-map-04.png)
    
    **Remarque :** il s'agit du même assistant que l'utilisation de **Créer une page** dans une application existante.
    
5.  Entrez **Carte des aéroports** comme nom de page. (Avec cet assistant, le nom de page sera également utilisé comme nom de la région de carte créée dans la page.) Cliquez sur l'icône à droite de l'entrée de table pour sélectionner la table **EBA\_SAMPLE\_MAP\_AIRPORTS**. Pour la colonne de géométrie, sélectionnez **GEOMETRY**, puis sélectionnez une colonne pour utiliser une info-bulle lorsque vous placez le pointeur de la souris sur un élément de la carte. ![Créer une application - Page Créer une carte](images/create-map-05.png)
    
6.  Observez que votre nouvelle page est désormais répertoriée sous **Pages**. Cliquez sur **Créer une application**. ![Créer une application - Finaliser la création de l'application](images/create-map-06.png)
    
7.  Vous accédez à la page sur laquelle vous gérez votre nouvelle application. Cliquez sur **Exécuter l'application**. ![Exécuter l'application](images/create-map-07.png)
    
8.  Connectez-vous à votre application à l'aide de votre nom utilisateur et de votre mot de passe de connexion APEX. ![Connexion à votre application](images/create-map-08.png)
    
9.  La présentation par défaut que nous avons sélectionnée pour notre application fournit une page d'accueil avec des liens vers d'autres pages. A partir de la page d'accueil, accédez à la page que vous venez de créer. ![Page d'accueil d'application](images/create-map-09.png)
    
10.  Observez que la page inclut une carte interactive indiquant les emplacements des aéroports avec des info-bulles telles que configurées. ![Voir la carte](images/create-map-10.png)
    

## Tâche 2 : inspecter la page Map

Vous allez maintenant inspecter la région Map créée par l'assistant.

1.  Dans la barre d'outils du Developer en bas de la page, cliquez sur le bouton **Page 2** pour modifier la page. ![Modifier la page](images/create-map-11.png)
    
2.  Dans l'arborescence de la page de gauche, sous **Corps**, cliquez sur **Carte des aéroports**. Il s'agit du titre de la région de carte créée par l'assistant Créer une page. Il est, par défaut, identique au titre de la page et peut être modifié selon vos besoins. Dans le panneau Détails de la région à droite, notez que cette région a le type **Carte**. ![Afficher les propriétés de la page](images/create-map-12.png)
    
3.  Les régions de carte incluent des couches qui correspondent aux points, lignes et polygones (d'Oracle Spatial, GeoJSON ou coordonnées) affichés en haut d'une carte d'arrière-plan. Lors de l'exécution pas à pas de l'assistant Créer une page, vous avez sélectionné une carte à l'aide de la colonne GEOMETRY de la table EBA\_SAMPLE\_MAP\_AIRPORTS (données Oracle Spatial). L'assistant a donc créé une couche contenant ces emplacements d'aéroport. Par défaut, la couche porte le même nom que la page, c'est-à-dire **Carte des aéroports**. Cela peut être modifié comme vous le souhaitez.
    
    Pour inspecter cette couche, dans l'arborescence Page du panneau de gauche, sous Couches, cliquez sur **Carte des aéroports**. Les détails de configuration sont affichés dans le panneau **Couche** à droite. Pour plus d'informations sur les éléments de configuration, cliquez sur l'onglet **Aide** dans le panneau central. Lorsque vous cliquez ensuite sur les éléments de configuration, des informations d'aide s'affichent pour cet élément. Par exemple, cliquez dans le menu **Type de couche** pour afficher de l'aide sur ses options. ![Inspecter les propriétés de couche de carte](images/create-map-13.png)
    
4.  Faites défiler le panneau Couche vers le bas pour voir les autres options de configuration définies par l'assistant, y compris le mapping de colonne où le type de données de géométrie est défini. Ici, vous utilisez le type de données spatiales natif d'Oracle, SDO\_GEOMETRY, et le nom de colonne est GEOMETRY. ![Inspecter les propriétés de couche de carte](images/create-map-14.png)
    

Félicitations pour la création de vos premières cartes. Il y a beaucoup de capacités au-delà des bases que vous venez d'explorer. N'hésitez pas à tester les ajustements des paramètres, puis enregistrez et exécutez pour afficher les résultats. Dans l'exercice suivant, vous allez configurer une nouvelle région de carte à partir de zéro.

Ceci conclut le laboratoire. Vous pouvez maintenant passer à l'exercice suivant.

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, Database Product Management, mars 2023