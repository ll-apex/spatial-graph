# Accédez à JupyterLab

## Présentation

Les blocs-notes sont des documents interactifs pour le code, le texte descriptif et les visualisations. Dans cet atelier, vous allez utiliser la version open source JupyterLab qui fournit un environnement de bloc-notes Web avec de nombreuses fonctionnalités conviviales telles que le téléchargement de fichiers.

Temps de laboratoire estimé : 5 minutes

### Objectifs

*   Vérifier l'accès à JupyterLab
*   Découvrir la fonctionnalité de bloc-notes
*   Sélectionner une option pour effectuer le reste des exercices pratiques

## Tâche 1 : extraction de l'adresse IP pour JupyterLab

1.  Dans le menu principal, accédez à Compute > Instances.

![Récupérer l'adresse IP](images/compute-01.png)

2.  Sur la page d'instructions de l'atelier, cliquez sur **Visualiser les informations de connexion** en haut à gauche et copiez le nom du compartiment.

![Récupérer l'adresse IP](images/compartment.png)

1.  Dans la console OCI, collez le nom de votre compartiment et sélectionnez-le dans la liste déroulante.

![Récupérer l'adresse IP](images/compute-02.png)

4.  Notez l'adresse IP publique de votre instance de calcul. JupyerLab a été défini sur cette instance. Vous l'utiliserez plus tard dans cet exercice et dans d'autres exercices.

![Récupérer l'adresse IP](images/compute-03.png)

## Tâche 2 : vérifier l'accès à JupyterLab

1.  Ouvrez un nouvel onglet de navigateur et entrez l'URL **http ://\[adresse IP\] :8001/lab** où \[adresse IP\] est l'adresse extraite dans la tâche 1.
    
    ![Accédez à JupyterLab](images/access-jupyter-01.png)
    
2.  Entrez le mot de passe **livelabs** et cliquez sur **Log in**.
    

## Tâche 2 : Explorer les blocs-notes Jupyter

Jupyter Notebook est un outil Web interactif qui vous permet de créer et de partager des documents contenant du code en direct, des équations, des visualisations et du texte. Il est largement utilisé dans la communauté de la science des données pour le prototypage et l'analyse de données.

Dans cette tâche, nous passerons en revue les bases de l'utilisation de Jupyter Notebook.

1.  Créez un bloc-notes.
    
    Lorsque votre environnement Jupyter se charge, vous devriez voir un onglet de lancement ouvert.
    
    ![L'onglet Lanceur est ouvert](./images/launcher1.png)
    
    Si la fenêtre du lanceur ne s'affiche pas, sélectionnez le fichier en haut à gauche de la fenêtre et sélectionnez "Nouveau lanceur".
    
    ![Ouvrir un nouvel onglet du lanceur](./images/launcher2.png)
    
    Dans la fenêtre du lanceur, sélectionnez "Python 3" pour créer un nouveau bloc-notes à l'aide du langage de programmation Python. Un nouveau bloc-notes est créé et vous pouvez commencer à travailler dessus en entrant du code dans les cellules de code ou en ajoutant du texte de démarque dans les cellules de démarque.
    
    ![créer un bloc-notes Python](./images/launcher3.png)
    
2.  Ajoutez du texte de démarque.
    
    Cliquez sur la cellule de code et utilisez le menu déroulant Utiliser le type de cellule pour sélectionner "Markdown"
    
    ![Ajouter une cellule de démarque](./images/notebook1.png)
    
    Collez ce qui suit dans la cellule et cliquez sur le bouton de lecture dans la barre d'outils, ou appuyez sur Shift+Enter pour exécuter la cellule.
    
        	<copy>
        	# My First Notebook
        	This is my first Jupyter notebook
        	</copy>
        
    
    ![Résultat de la démarque](./images/notebook2.png)
    
3.  Écrivez du code Python. Collez ce qui suit dans la cellule suivante et exécutez-le. La phrase "Bonjour, Monde !" doit apparaître sous la cellule.
    
        	<copy>
        	print('Hello, World!')
        	</copy>
        
        
    
    ![Hello World exemple](./images/notebook3.png)
    
4.  To save a Jupyter Notebook, click on the "Save" icon on the toolbar, or press Ctrl+S (or Cmd+S on macOS). The notebook will be saved with the .ipynb file extension.
    

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Contributeurs** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Dernière mise à jour par/date** - David Lapp, août 2023