# Créer le graphe

## Présentation

Désormais, les tables sont créées et alimentées avec des données. Créons une représentation graphique de ces éléments.

Durée estimée : 5 minutes

### Objectifs

Découvrez comment créer un graphique à partir de sources de données relationnelles :

*   Démarrage d'un client (shell Python) qui se connecte au serveur Graph
*   Utiliser le langage DDL (Data Definition Language) PGQL (par exemple, CREATE PROPERTY GRAPH) pour instancier un graphique

### Prérequis

*   Cet exercice suppose que vous avez terminé l'exercice : Créer et alimenter des tables.

## Tâche 1 : démarrer le client Python

Connectez-vous à l'instance de calcul via SSH en tant qu'utilisateur **opc** à l'aide de la clé privée que vous avez créée précédemment.

    <copy>
    ssh -i <private_key> opc@<public_ip_for_compute>
    </copy>
    

Exemple :

    <copy>
    ssh -i key.pem opc@203.0.113.14
    </copy>
    

Démarrez une instance de shell client Python qui se connecte au serveur.

    <copy>
    opg4py -b https://localhost:7007 -u customer_360
    </copy>
    

Vous devez voir ce qui suit si le shell client démarre correctement.

    <copy>
    password:
    
    Oracle Graph Client Shell 22.4.0
    >>>
    </copy>
    

## Tâche 2 : créer un graphique

Configurez l'instruction de création de graphe de propriétés, qui crée un graphe à partir des tables existantes.

    <copy>
    statement = '''
    CREATE PROPERTY GRAPH "customer_360"
      VERTEX TABLES (
        customer
      , account
      , merchant
      )
      EDGE TABLES (
        account
          SOURCE KEY(id) REFERENCES account (id)
          DESTINATION KEY(customer_id) REFERENCES customer (id)
          LABEL owned_by PROPERTIES (id)
      , parent_of
          SOURCE KEY(customer_id_parent) REFERENCES customer (id)
          DESTINATION KEY(customer_id_child) REFERENCES customer (id)
      , purchased
          SOURCE KEY(account_id) REFERENCES account (id)
          DESTINATION KEY(merchant_id) REFERENCES merchant (id)
      , transfer
          SOURCE KEY(account_id_from) REFERENCES account (id)
          DESTINATION KEY(account_id_to) REFERENCES account (id)
      ) 
    '''
    </copy>
    

Pour plus d'informations sur la syntaxe DDL, reportez-vous à [pgql-lang.org](https://pgql-lang.org/spec/1.4/#create-property-graph). Notez que _toutes les colonnes des tables d'entrée sont mises en correspondance avec les propriétés des sommets/arêtes [par défaut](https://pgql-lang.org/spec/1.4/#properties)_. Pour l'arête **owned\_by**, seule la propriété **id** est indiquée avec le mot-clé **PROPERTIES** à des fins de génération d'ID d'arête et les autres propriétés ne sont pas indiquées, car elles sont déjà bloquées par les sommets du compte.

Exécutez maintenant le script DDL PGQL pour créer le graphique.

    >>> <copy>session.prepare_pgql(statement).execute()</copy>
    False   # This is the expected result
    

## Tâche 3 : vérifier le graphique que vous venez de créer

Vérifiez que le graphique a été créé. Copiez, collez et exécutez les instructions suivantes dans le shell Python.

Joignez le graphique.

    >>> <copy>graph = session.get_graph("customer_360")</copy>
    

Vérifiez que le graphique a été créé.

    >>> <copy>graph</copy>
    PgxGraph(name: customer_360, v: 15, e: 24, directed: True, memory(Mb): 0)
    

Exécutez des requêtes PGQL. Par exemple, la liste des étiquettes de sommet :

    <copy>
    graph.query_pgql("""
      SELECT DISTINCT LABEL(v) FROM MATCH (v)
    """).print()
    </copy>
    
    +----------+
    | LABEL(v) |
    +----------+
    | ACCOUNT  |
    | CUSTOMER |
    | MERCHANT |
    +----------+
    

Combien de sommets avec chaque libellé :

    <copy>
    graph.query_pgql("""
      SELECT COUNT(v), LABEL(v) FROM MATCH (v) GROUP BY LABEL(v)
    """).print()
    </copy>
    
    +---------------------+
    | COUNT(v) | LABEL(v) |
    +---------------------+
    | 5        | MERCHANT |
    | 6        | ACCOUNT  |
    | 4        | CUSTOMER |
    +---------------------+
    

Liste des libellés d'arête :

    <copy>
    graph.query_pgql("""
      SELECT DISTINCT LABEL(e) FROM MATCH ()-[e]->()
    """).print()
    </copy>
    
    +-----------+
    | LABEL(e)  |
    +-----------+
    | OWNED_BY  |
    | PARENT_OF |
    | PURCHASED |
    | TRANSFER  |
    +-----------+
    

Combien d'arêtes avec chaque étiquette :

    <copy>
    graph.query_pgql("""
      SELECT COUNT(e), LABEL(e) FROM MATCH ()-[e]->() GROUP BY LABEL(e)
    """).print()
    </copy>
    
    +----------------------+
    | COUNT(e) | LABEL(e)  |
    +----------------------+
    | 4        | OWNED_BY  |
    | 8        | TRANSFER  |
    | 1        | PARENT_OF |
    | 11       | PURCHASED |
    +----------------------+
    

## Tâche 4 : publier le graphique

Le graphique nouvellement créé est "privé" par défaut et n'est accessible qu'à partir de la session en cours. Pour accéder au graphique à partir de nouvelles sessions à l'avenir, vous pouvez le publier.

Ensuite, créez à nouveau le graphique en suivant la procédure ci-dessus, puis publiez-le.

    <copy>
    graph.publish()
    </copy>
    

Lors de la prochaine connexion, vous pourrez accéder au graphique conservé sur la mémoire sans le recharger, si le serveur de graph n'a pas été arrêté ou redémarré entre les connexions.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

Vous êtes autorisé à publier des graphiques car le rôle **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** a été accordé lors de la création de l'utilisateur. Sinon, l'utilisateur **ADMIN** doit l'accorder et se reconnecter au shell Python pour récupérer les droits d'accès mis à jour.

Vous pouvez maintenant passer à l'exercice suivant.

## Accusés de réception

*   **Auteur** - Jayant Sharma
*   **Contributeurs** - Arabella Yao, Jenny Tsai
*   **Dernière mise à jour par/date** - Ryota Yamanaka, mars 2023