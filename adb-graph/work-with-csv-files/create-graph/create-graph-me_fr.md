# Créer un graphe

## Présentation

Dans cet exercice, vous allez créer un graphique à partir des tables `bank_accounts` et `bank_txns` à l'aide de Graph Studio et de l'instruction CREATE PROPERTY GRAPH.

Temps estimé : 15 minutes.

Regardez la vidéo ci-dessous pour une présentation rapide du laboratoire. [Procédure pas à pas](videohub:1_j5xjw77c)

### Objectifs

Découvrez comment :

*   Utiliser Graph Studio et PGQL DDL (instruction CREATE PROPERTY GRAPH) pour modéliser et créer un graphique à partir de tables ou de vues existantes.

### Prérequis

*   L'exercice suivant nécessite un compte Autonomous Database - Infrastructure partagée.
*   Et que l'utilisateur compatible Graph (`GRAPHUSER`) existe. En d'autres termes, il existe un utilisateur de base de données doté des rôles et privilèges appropriés.

## Tâche 1 : créer un graphique de comptes et de transactions

1.  Cliquez sur l'icône **Graphique** pour accéder à la création du graphique.  
    Cliquez ensuite sur **Créer un graphique**.
    
    ![Indique où se trouve le modélisateur de boutons de création](images/graph-create-button.png " ")
    
2.  Entrez `bank_graph` comme nom de graphique, puis cliquez sur **Suivant**. Les champs de description et de balises sont facultatifs.  
    Ce nom de graphique est utilisé au cours de l'exercice suivant.  
    N'entrez pas un nom différent car les requêtes et les fragments de code de l'exercice suivant échoueront.
    
    ![Affiche la fenêtre de création de graphique dans laquelle vous affectez un nom au graphique](./images/create-graph-dialog.png " ")
    
3.  Développez **GRAPHUSER** et sélectionnez les tables `BANK_ACCOUNTS` et `BANK_TXNS`.
    
    ![Montre comment sélectionner BANK_ACCOUNTS et BANK_TXNS](./images/select-tables.png " ")
    
4.  Déplacez-les vers la droite, c'est-à-dire cliquez sur la première icône de la commande de navette.
    
    ![Affiche les tables sélectionnées](./images/selected-tables.png " ")
    
5.  Cliquez sur **Suivant**. Nous allons modifier et mettre à jour ce graphique pour ajouter un bord et un libellé de sommet.
    
    Le graphique suggéré comporte `BANK_ACCOUNTS` comme table de sommets car des contraintes de clé étrangère sont spécifiées sur `BANK_TXNS` qui le référencent.
    
    `BANK_TXNS` est un tableau d'arêtes suggéré.
    
    ![Affiche le tableau des sommets et des arêtes](./images/create-graph-suggested-model.png " ")
    
6.  Nous allons maintenant modifier les libellés Vertex et Edge par défaut.
    
    Cliquez sur la table de sommets `BANK_ACCOUNTS`. Remplacez le libellé de sommet par **ACCOUNTS**. Cliquez ensuite sur la coche pour confirmer le libellé et enregistrer la mise à jour.
    
    ![Modification du nom de libellé du sommet en Comptes](images/edit-accounts-vertex-label.png " ")
    
    Cliquez sur la table d'arêtes `BANK_TXNS` et renommez le libellé d'arête `BANK_TXNS` en **TRANSFERS**. Cliquez ensuite sur la coche pour confirmer le libellé et enregistrer la mise à jour.
    
    ![Modification du nom d'étiquette de l'arête en Transferts](images/edit-edge-label.png " ")
    
    Cela est **important** car nous allons utiliser ces libellés d'arête dans l'exercice suivant de cet atelier lors de l'interrogation du graphique. Cliquez sur **Suivant**.
    

7.  A l'étape Récapitulatif, cliquez sur **Créer un graphique**. Cela ouvrira un onglet Créer un graphique, cliquez sur \*\*Créer un graphique.
    
    ![Affiche l'onglet du travail dont le statut est Succès](./images/jobs-create-graph.png " ")
    
    L'onglet Créer un graphique s'ouvre. Cliquez sur **Créer un graphique**.
    
    ![Affiche la mémoire activée et le bouton Créer un graphique](./images/create-graph-in-memory.png " ")
    
    Ensuite, vous accédez à la page Jobs sur laquelle le graphique sera créé.
    
    Ceci conclut ce laboratoire. **Vous pouvez maintenant passer à l'exercice suivant.**
    

## Accusés de réception

*   **Auteur** - Jayant Sharma, Product Management
*   **Contributeurs** - Jayant Sharma, Product Management
*   **Dernière mise à jour par/date** - Ramu Murakami Gutierrez, chef de produit, juin 2023