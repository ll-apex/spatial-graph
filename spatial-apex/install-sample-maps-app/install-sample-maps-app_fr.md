# Installer l'application Sample Maps

## Présentation

Oracle APEX permet d'accéder à un portefeuille d'exemples d'applications qui mettent en évidence des domaines de fonctionnalité spécifiques. L'application Sample Maps présente notamment les fonctionnalités de mise en correspondance dans Oracle APEX. Une grande variété d'exemples sont fournis pour servir d'exemples fonctionnels et de points de départ pour une personnalisation ultérieure. Dans cet exercice, vous allez installer et configurer l'application Sample Maps.

Temps de laboratoire estimé : 15 minutes

### Objectifs

*   Installer l'application Sample Maps
*   Charger les données de prise en charge

### Prérequis

*   Oracle APEX 21.1+ est requis. Les captures d'écran de cet atelier sont réalisées à l'aide d'APEX 21.2. Etant donné que nous recommandons généralement d'utiliser la [dernière version d'APEX](https://www.oracle.com/tools/downloads/apex-downloads/), attendez-vous à de petites différences occasionnelles dans l'interface utilisateur.

## Tâche 1 : installer l'application

1.  Commencez par cliquer sur **App Builder**.
    
    ![Application Builder APEX](images/install-sample-maps-00.png)
    
2.  Cliquez sur **Installer une application échantillon ou de départ**.
    
    ![Sélectionner une application échantillon ou de départ](images/install-sample-maps-01.png)
    
    **Remarque :** si votre espace de travail comporte des applications existantes, cliquez sur **Créer**, puis sur **Starter App**.
    
3.  Cliquez sur **Exemples** pour ouvrir un nouvel onglet de navigateur avec la liste des exemples d'applications disponibles.
    
    ![Sélectionner des échantillons](images/install-sample-maps-02.png)
    
4.  Faites défiler la page jusqu'à **Exemples de cartes** et cliquez sur **Télécharger l'application**.
    
    ![Texte de remplacement de l'image](images/install-sample-maps-03.png)
    
    Vous serez invité à enregistrer le groupe d'applications dans un dossier local.
    
    **Remarque :** si vous êtes redirigé vers github, accédez au dossier de votre version APEX et téléchargez **sample-maps.zip**.
    
5.  Revenez à l'onglet du navigateur App Builder en cliquant sur **Importer**.
    
    ![Sélectionner un import](images/install-sample-maps-04.png)
    
6.  Glissez-déplacez ou accédez au fichier ZIP de l'application Sample Maps que vous avez téléchargé précédemment. Laissez le type de fichier sélectionné en tant qu'application de base de données, puis cliquez sur **Suivant**.
    
    ![Sélectionner le code postal de l'application Sample Maps](images/install-sample-maps-05.png)
    
7.  L'importation du fichier est confirmée. Cliquez à nouveau sur **Suivant**.
    
    ![Cliquez sur Suivant](images/install-sample-maps-06.png)
    
8.  Laissez les sélections de menu par défaut et cliquez sur **Installer l'application**.
    
    ![Cliquez sur Installer l'application](images/install-sample-maps-07.png)
    
    Vous accédez alors à l'assistant Install Application.
    
9.  Laissez les sélections de menu par défaut et cliquez sur **Suivant**.
    
    ![Cliquez sur Suivant](images/install-sample-maps-08.png)
    
10.  Cliquez sur **Suivant** pour valider la compatibilité du système.
    

![Cliquez sur Suivant](images/install-sample-maps-09.png)

11.  Lorsque la compatibilité est confirmée, cliquez sur **Installer** pour lancer l'installation des objets de base de données pris en charge et de l'application APEX.

![Cliquez sur Installer](images/install-sample-maps-10.png)

12.  Une fois l'installation terminée, cliquez sur **Run Application**.

![Cliquez sur Run Application (Lancer une application).](images/install-sample-maps-11.png)

13.  Connectez-vous à l'application Sample Maps à l'aide du nom utilisateur et du mot de passe de votre espace de travail APEX.

![Connexion](images/install-sample-maps-12.png)

## Tâche 2 : Charger des données

1.  Vous êtes maintenant dans l'application Sample Maps qui fournit de nombreux exemples de cartes et d'opérations spatiales dans APEX. Lors du lancement initial, un message d'avertissement concernant le chargement des données s'affiche. Cliquez sur le lien **Chargement des données** dans ce message. Vous accéderez à une page où vous terminerez le chargement des données de démonstration.
    
    ![Cliquer sur Chargement des données](images/install-sample-maps-13.png)
    
2.  La page Chargement des données affiche le statut de chargement des jeux de données States et Airports utilisés par l'application Sample Maps et le reste de cet atelier. Lors de l'installation de l'application Sample Maps, ces jeux de données ne sont que partiellement chargés. Pour terminer le chargement des données échantillon, vous pouvez soit charger directement à partir des fichiers stockés dans github, soit télécharger les fichiers et les charger à partir de votre système local. Si vous exécutez APEX sur un réseau qui nécessite un proxy pour accéder à github, vous devez utiliser cette dernière option.
    
    Si votre instance APEX ne nécessite pas de proxy pour accéder à github (par exemple, apex.oracle.com ou APEX avec Oracle Autonomous Database), cliquez sur le bouton pour charger **Directly à partir de GitHub**, puis cliquez sur **Charger l'ensemble de données** en haut à droite.
    
    ![Cliquez directement sur Github](images/install-sample-maps-14.png)
    
    Si votre instance APEX nécessite un proxy pour accéder à github (par exemple, APEX exécuté derrière votre pare-feu d'entreprise) ou si vous rencontrez d'autres problèmes lors du chargement directement à partir de github, cliquez sur le bouton **Télécharger des fichiers** qui fournit d'autres instructions.
    
3.  Une fois le chargement des données terminé, une notification apparaît en haut à droite et le message d'avertissement disparaît. L'application Sample Maps est maintenant prête à être utilisée.
    
    ![Confirmation du chargement des données](images/install-sample-maps-15.png)
    

## Tâche 3 : Examiner l'exemple d'application Maps

1.  Cliquez sur l'une des mosaïques pour accéder à la page associée dans l'application. Par exemple, cliquez sur **Carte et rapport**.
    
    ![Accéder à la page Carte et état](images/install-sample-maps-16.png)
    
2.  Dans cette page, le fait de cliquer sur un élément dans le rapport de droite est centré sur l'élément dans la carte et ouvre une fenêtre d'informations. Cliquez sur l'icône dans le coin supérieur gauche pour ouvrir un panneau de navigation permettant d'accéder à d'autres pages de l'application.
    
    ![Interagir avec la carte](images/install-sample-maps-17.png)
    
3.  Cliquez sur les éléments du panneau de navigation pour accéder aux autres pages de l'application.
    
    ![Le panneau de navigation affiche d'autres pages](images/install-sample-maps-18.png)
    
4.  Pour fermer le panneau de navigation, cliquez sur l'icône en haut à gauche. Vous pouvez également accéder à la page d'accueil de l'application en cliquant sur **Exemples de correspondance** en haut à gauche.
    
    ![Fermer le panneau de navigation](images/install-sample-maps-19.png)
    

## Tâche 4 : Explorer les données de démonstration

1.  Revenez à APEX, cliquez sur **SQL Workshop**, puis sur **Object Browser**.
    
    ![SQL Workshop - Object Browser (Navigateur d'objet)](images/install-sample-maps-20.png)
    
2.  Observez les tables créées lors de l'étape de chargement des données effectuée précédemment. Cliquez sur **EBA\_SAMPLE\_MAP\_AIRPORTS**. Notez que les colonnes incluent une colonne nommée GEOMETRY de type SDO\_GEOMETRY (type de données spatiales natives d'Oracle).
    
    ![Table avec colonne de géométrie native](images/install-sample-maps-21.png)
    
3.  Cliquez sur l'onglet **Données** pour afficher le contenu de la table.
    
    ![Contenu de la table](images/install-sample-maps-22.png)
    
    Faites ensuite défiler l'affichage vers la droite pour voir la colonne de géométrie. Les aéroports étant stockés en tant que points, APEX affiche une représentation en chaîne de la valeur de géométrie de point. Les points sont toujours basés sur une seule coordonnée. Il est donc logique qu'APEX affiche la valeur de cette façon.
    
    ![géométries de point](images/install-sample-maps-23.png)
    
4.  Cliquez sur **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES**. Notez à nouveau que les colonnes incluent une colonne nommée GEOMETRY de type SDO\_GEOMETRY (type de données spatiales natives d'Oracle).
    
    ![Table avec colonne de géométrie native](images/install-sample-maps-24.png)
    
5.  Cliquez sur l'onglet **Données** pour visualiser le contenu de la table. Comme cette table stocke les états, les géométries sont des polygones. APEX n'affiche pas de représentation sous forme de chaîne de ces valeurs, car il peut s'agir d'ensembles de coordonnées extrêmement longs.
    
    ![Géométries de polygone](images/install-sample-maps-25.png)
    
6.  Observez les tables portant des noms tels que **MDRT\_....$**. Elles sont créées et gérées automatiquement en arrière-plan par la base de données pour prendre en charge les index spatiaux sur d'autres tables. Vous ne pouvez jamais créer, mettre à jour ou supprimer manuellement ces tables. Ils servent uniquement à soutenir les opérations d'analyse spatiale et peuvent être ignorés.
    
    ![Artefacts d'index spatial](images/install-sample-maps-26.png)
    
7.  Enfin, vous pouvez exécuter une requête spatiale de base avec ces données. Cliquez sur **SQL Workshop**, puis sur **Commandes SQL**.
    
    ![SQL Workshop - Commandes SQL](images/install-sample-maps-27.png)
    
8.  La requête suivante renvoie le nombre d'aéroports avec une couverture terrestre de plus de 1000 acres qui se trouvent à moins de 100 km du Texas. Notez l'utilisation de l'opérateur spatial natif **sdo\_within\_distance**. Copiez et collez la requête dans la fenêtre Commandes SQL, puis cliquez sur **Exécuter** en haut à droite.
    
        <copy>
        select count(a.id) as number_of_airports
        from EBA_SAMPLE_MAP_AIRPORTS a,
              EBA_SAMPLE_MAP_SIMPLE_STATES b
        where b.state_code= 'TX'
           and land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance=100 unit=KM') = 'TRUE'
        </copy>
        
    
    ![Requête spatiale](images/install-sample-maps-28.png)
    
9.  Dans l'opérateur sdo\_within\_distance, mettez à jour la distance à 300 km et réexécutez-la. Observez les changements de résultat en fonction de la zone de recherche plus large.
    
    ![Requête spatiale](images/install-sample-maps-29.png)
    

Dans un exercice ultérieur, vous configurerez une carte qui affiche les résultats de cette requête, où l'état et la distance sont contrôlés par les menus de la page.

Vous avez maintenant installé et exploré l'application Sample Maps et les données. Ensuite, vous allez commencer à créer votre propre application et vos propres cartes.

Ceci conclut le laboratoire. Vous pouvez maintenant passer à l'exercice suivant.

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Contributeurs** - Carsten Czarski, Développement APEX, Oracle
*   **Dernière mise à jour par/date** - David Lapp, Database Product Management, mars 2023