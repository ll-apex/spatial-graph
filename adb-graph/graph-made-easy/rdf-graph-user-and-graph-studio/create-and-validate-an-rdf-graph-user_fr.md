# Créer un graphe RDF dans Graph Studio

## Présentation

Graph Studio dans Oracle Autonomous Database permet aux utilisateurs de modéliser, de créer, d'interroger et d'analyser des données de graphique. Il comprend des blocs-notes, des API de développeur pour l'exécution de requêtes de graphique à l'aide de PGQL, plus de 60 algorithmes de graphique intégrés, et offre des dizaines de visualisations, y compris la visualisation de graphique native. En plus du graphique de propriétés, Graph Studio étend désormais la prise en charge des technologies sémantiques, y compris les capacités de stockage, d'inférence et de requête pour les données et les ontologies basées sur Resource Description Framework (RDF) et Web Ontology Language (OWL). Vous pouvez désormais utiliser Graph Studio pour les fonctions RDF prises en charge suivantes :

*   Créer un graphe RDF
*   Exécuter des requêtes SPARQL sur le graphique RDF dans un paragraphe de bloc-notes
*   Analyser et visualiser les graphiques RDF

Durée estimée : 5 minutes

Regardez la vidéo ci-dessous pour une présentation rapide du laboratoire. [Créer un graphique RDF dans Graph Studio](videohub:1_vvqhh26v)

### Objectifs

*   Créer un graphique RDF dans Graph Studio
*   Valider le graphique RDF
*   Exécuter des requêtes SPARQL sur la page Playground

### Prérequis

*   L'exercice suivant nécessite une instance Autonomous Database - Serverless.
*   Et que l'utilisateur compatible Graph (GRAPHUSER) existe. En d'autres termes, il existe un utilisateur de base de données doté des rôles et privilèges appropriés.

## Tâche 1 : créer un graphe RDF dans Graph Studio

En supposant que vous avez terminé les exercices précédents et que vous êtes actuellement connecté, procédez comme suit :

1.  Cliquez sur **Graphiques** dans le menu de navigation à gauche pour accéder à la page Graphiques.

![La page de destination après la création de l'environnement est le menu des travaux](./images/graph-studio-home.png)

2.  Dans le menu déroulant Type de graphique, sélectionnez **RDF**, puis cliquez sur le bouton **Créer** dans l'angle supérieur droit de l'interface.

![Le menu déroulant Type de graphique de la page Graph Studio affiche les options de graphique PG et RDF](./images/graph-studio-graphs.png)

3.  Sélectionnez **Graphique RDF**, puis cliquez sur le bouton **Confirmer**.

![bouton de confirmation pour sélectionner l'option de graphique RDF](./images/click-confirm-rdf.png)

4.  L'assistant Créer un graphique RDF s'ouvre comme suit :

![Page "Créer un graphique RDF".](./images/create-rdf-graph.png)

5.  Entrez le chemin d'URI OCI Object Storage :
    
          <copy>https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt
        
6.  Cliquez sur **Aucune information d'identification**.
    
7.  Cliquez sur **Suivant**. La boîte de dialogue suivante doit apparaître. Saisissez "MOVIESTREAM" dans le champ Graph Name :
    

![Deuxième page "Créer un graphique RDF"](./images/create-rdf-graph-2.png)

8.  Cliquez sur **Créer**.
    
    Le travail de création de graphique RDF sera lancé. Comme le fichier RDF contient 139461 enregistrements, le processus peut prendre de 3 à 4 minutes. Vous pouvez surveiller le travail sur la page **Travaux** de Graph Studio.
    

![La page "Travaux"de Graph Studio affiche un travail"Créer un graphique RDF - MOVIESTREAM" toujours en cours](./images/graph-studio-jobs.png)

    When succeeded, the status will change from pending to succeeded and Logs can be viewed by clicking on the three dots on the right side of the job row and selecting **See Log**. The log for the job displays details as shown below:
    
    ```
    Tue, Mar 1, 2022 08:21:04 AM
    Finished execution of task Graph Creation - MOVIESTREAM.
    
    Tue, Mar 1, 2022 08:21:04 AM
    Graph MOVIESTREAM created successfully
    
    Tue, Mar 1, 2022 08:21:04 AM
    Optimizer Statistics Gathered successfully
    
    Tue, Mar 1, 2022 08:20:50 AM
    External table <graph-user>_TAB_EXTERNAL dropped successfully
    
    Tue, Mar 1, 2022 08:20:49 AM
    Data successfully bulk loaded from ORACLE_ORARDF_STGTAB
    
    Tue, Mar 1, 2022 08:20:39 AM
    Model MOVIESTREAM created successfully
    
    Tue, Mar 1, 2022 08:20:37 AM
    Network RDF_NETWORK created successfully
    
    Tue, Mar 1, 2022 08:20:24 AM
    Data loaded into the staging table ORACLE_ORARDF_STGTAB from <graph-user>_TAB_EXTERNAL
    
    Tue, Mar 1, 2022 08:20:19 AM
    External table <graph-user>_TAB_EXTERNAL created successfully
    
    Tue, Mar 1, 2022 08:20:19 AM
    Using the Credential MOVIES_CREDENTIALS
    
    Tue, Mar 1, 2022 08:20:19 AM
    Started execution of task Graph Creation - MOVIESTREAM.
    ```
    

## Tâche 2 : valider le graphique RDF

Vous pouvez explorer et valider le graphique RDF que vous venez de créer sur la page **Graphiques** de Graph Studio, comme indiqué ci-dessous :

1.  Accédez à la page **Graphiques** et définissez le **type de graphique** sur RDF à l'aide du menu déroulant. Sélectionnez la ligne de graphique MOVIESTREAM parmi les graphiques RDF disponibles, des exemples d'instruction (des triples ou des quadrillages doivent apparaître), utilisez les trois points horizontaux pour redimensionner ces instructions et les mettre en vue. Des exemples d'instruction (triple ou quadruple) à partir du graphique RDF sont affichés dans le panneau inférieur comme indiqué :

![Des exemples d'instructions du graphique RDF 'MOVIESTREAM' sont affichés en triplets](./images/graph-sample-statements.png)

2.  Après avoir sélectionné le graphique MOVIESTREAM, faites défiler la page jusqu'en bas et vérifiez que 500 lignes de triples RDF ont été extraites.

![Exemples d'instruction à partir du graphique MOVIESTREAM RDF](./images/sample-statements.png)

## Tâche 3 : exécuter des requêtes SPARQL sur la page de terrain de jeu

Vous pouvez exécuter des requêtes SPARQL sur le graphique RDF à partir de la page **Zone de lecture de requête**.

1.  Sur la page **Graphiques**, sélectionnez **RDF** dans le menu déroulant Type de graphique et cliquez sur le bouton **Requête** pour accéder à la page Zone de lecture de requête.

![Page Graphiques avec le type de graphique RDF sélectionné et le bouton de requête mis en surbrillance](./images/graph-type.png)

2.  Si vous avez plusieurs graphiques dans Graph Studio, vous devrez choisir le graphique à interroger. Dans le menu Graph Name, sélectionnez MOVIESTREAM dans le menu déroulant.

![Le champ de lecture de requête affiche le nom de graphique 'MOVIESTREAM' sélectionné dans le menu déroulant](./images/query-playground.png)

3.  Exécutez la requête suivante pour le graphique RDF.
    
        <copy>PREFIX rdf: &lthttp://www.w3.org/1999/02/22-rdf-syntax-ns#&gt
        PREFIX rdfs: &lthttp://www.w3.org/2000/01/rdf-schema#&gt
        PREFIX xsd: &lthttp://www.w3.org/2001/XMLSchema#&gt
        PREFIX ms: &lthttp://www.example.com/moviestream/&gt
        
        SELECT DISTINCT ?gname
        WHERE {
          ?movie ms:actor/ms:name "Keanu Reeves" ;
          ms:genre/ms:genreName ?gname .
        }
        ORDER BY ASC(?gname)<copy>
        
    
    Lorsque la requête est exécutée avec succès, la sortie de la requête s'affiche comme suit :
    

![Le champ de lecture de requête affiche l'exécution réussie d'une requête sur le graphique RDF MOVIESTREAM et affiche les résultats de la requête](./images/query-playground-script.png)

Ceci conclut ce laboratoire. **Vous pouvez maintenant passer à l'exercice suivant.**

## Accusés de réception

*   **Auteur** - Malia German, Ethan Shmargad, Matthew McDaniel Ingénieurs solutions, Ramu Murakami Gutierrez Chef de produit
*   **Contributeur technique** - Melliyal Annamalai Chef de produit distingué, Joao Paiva Consulting Membre du personnel technique, Lavanya Jayapalan Développeur principal d'assistance utilisateur
*   **Dernière mise à jour par/date** - Ramu Murakami Gutierrez, chef de produit, août 2023