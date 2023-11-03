# Visualiser le graphique

## Présentation

Les résultats des analyses effectuées dans les exercices précédents peuvent être facilement visualisés à l'aide de la fonctionnalité Visualisation de graphique.

Durée estimée : 5 minutes

La vidéo suivante présente le composant Visualisation de graphique (= GraphViz).

[YouTube](youtube:zfefKdNfAY4)

### Objectifs

*   Découvrez comment exécuter des requêtes graphiques PGQL et visualiser les résultats.

### Prérequis

*   Le graphe est créé et publié
*   Le serveur Graph (avec GraphViz) est en fonctionnement

## Tâche 1 : connectez-vous à GraphViz

Ouvrez GraphViz à l'adresse **`https://<public_ip_for_compute>:7007/ui`** à l'aide d'un navigateur Web. Remplacez **`<public_ip_for_compute>`** par celui de l'instance de calcul du serveur de graphe.

Etant donné que l'image Marketplace est distribuée avec un certificat SSL auto-signé, vous devez la modifier pour votre propre certificat en production. Pendant ce temps, les navigateurs Web devraient afficher des avertissements, alors que nous comprenons qu'il est sûr.

Si vous utilisez **Chrome**, saisissez **thisisunsafe** dans la fenêtre d'avertissement pour passer à l'écran GraphViz.

![Connexion-chrome](images/login-chrome.jpg)

A l'aide de **Firefox**, cliquez sur **Avancé**, puis sur **Accepter le risque et continuer**.

![connexion-firefox](images/login-firefox.jpg)

Vous devriez voir un écran similaire à la capture d'écran ci-dessous. Entrez le nom utilisateur (**customer\_360**) et le mot de passe, puis cliquez sur Soumettre. **Graph Server** est la valeur par défaut dans les options avancées. Vous n'avez donc pas besoin de la modifier.

![connexion](images/login.jpg)

## Tâche 2 : Modifier la requête

Modifiez la requête pour obtenir les 5 premières lignes, c'est-à-dire remplacez **LIMIT 100** par **LIMIT 5**, puis cliquez sur Exécuter.

Vous devriez voir un graphique similaire à la capture d'écran ci-dessous.

![afficher-5 éléments](images/show-5-elements.jpg)

## Tâche 3 : ajouter des points forts

Ajoutons maintenant des étiquettes et d'autres contextes visuels. Ce sont des faits saillants. Cliquez [ici](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/highlights.json.zip) pour télécharger un fichier ZIP, highlights.json.zip. Décompressez ce fichier et notez où il est décompressé.

Cliquez sur le bouton Charger sous **Paramètres** (à droite de l'écran). Accédez au dossier approprié, choisissez le fichier et cliquez sur Ouvrir pour le charger.

![faits saillants-1](images/highlights-1.png)

Le graphique devrait à présent ressembler à

![faits saillants-2](images/highlights-2.png)

## Tâche 4 : correspondance de modèle avec PGQL

1.  Ensuite, nous allons exécuter quelques requêtes PGQL.
    
    Le site [pgql-lang.org](http://pgql-lang.org) et la [spécification](http://pgql-lang.org/spec/1.4) sont les meilleures références pour obtenir des détails et des exemples. Pour les besoins de ce laboratoire, cependant, voici les bases minimales.
    
    La structure générale d'une requête PGQL est la suivante :
    
        <copy>
        SELECT <select_list>
        FROM MATCH <graph_pattern> ON <graph_name>
        WHERE <condition>
        </copy>
        
    
    PGQL fournit une structure spécifique appelée clause **MATCH** pour la mise en correspondance des modèles de graphique. Un modèle de graphique correspond aux sommets et aux arêtes qui répondent aux conditions et contraintes données.
    
    *   **(v)** indique une variable de sommet **v**
    *   **\-** indique une arête non dirigée, comme dans (source)-(dest)
    *   **\->** arête sortante de la source vers la destination
    *   **<-** arête entrante de la destination vers la source
    *   **\[e\]** indique une variable d'axe **e**
    
    En outre, omettez le fichier **graph\_name** ici, car il est sélectionné dans l'interface utilisateur GraphViz.
    
2.  Trouvons les comptes qui ont eu un transfert sortant et entrant de plus de 500 le même jour.
    
    La requête PGQL est la suivante :
    
        <copy>
        SELECT *
        FROM MATCH (a)-[t1:transfer]->(a1)
           , MATCH (a2)-[t2:transfer]->(a)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
        </copy>
        
    
    Dans la première clause **MATCH** ci-dessus, **(a)** indique le sommet source et **(a1)** la destination, tandis que **\[t1:transfer\]** est l'arête qui les relie. La commande **:transfer** spécifie que l'arête **t1** porte l'étiquette **TRANSFER**. La virgule (,) entre les deux modèles est une condition AND.
    
3.  Copiez et collez la requête dans la zone de saisie de texte Requête de graphique PGQL de l'application GraphViz. Cliquez sur Run (Exécuter).
    
    Le résultat doit se présenter comme indiqué ci-dessous. Dans les paramètres de mise en surbrillance, les comptes commençant par **xxx-yyy-** sont affichés en rouge (= comptes de la banque), tandis que **xxx-zzz-** sont affichés en orange (= comptes d'une autre banque).
    
    ![Transferts le même jour](images/same-day-transfers.jpg)
    
4.  La requête suivante recherche les modèles de transferts vers et depuis les deux mêmes comptes, c'est-à-dire à partir de a1->a2 et de a2->a1.
    
    La requête PGQL est la suivante :
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
        </copy>
        
5.  Copiez et collez la requête dans la zone de saisie de texte Requête de graphique PGQL de l'application GraphViz. Cliquez sur Run (Exécuter).
    
    Le résultat doit se présenter comme indiqué ci-dessous.
    
    ![cycle-2-hops](images/cycle-2-hops.jpg)
    
6.  Ajoutons un compte de plus à cette requête pour trouver un modèle de transfert circulaire entre 3 comptes.
    
    La requête PGQL devient :
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
        </copy>
        
7.  Copiez et collez la requête dans la zone de saisie de texte Requête de graphique PGQL de l'application GraphViz. Cliquez sur Run (Exécuter).
    
    Le résultat doit se présenter comme indiqué ci-dessous.
    
    ![cycle-3-hops](images/cycle-3-hops.jpg)
    

## Accusés de réception

*   **Auteur** - Jayant Sharma
*   **Contributeurs** - Arabella Yao, Jenny Tsai
*   **Dernière mise à jour par/date** - Ryota Yamanaka, mars 2023