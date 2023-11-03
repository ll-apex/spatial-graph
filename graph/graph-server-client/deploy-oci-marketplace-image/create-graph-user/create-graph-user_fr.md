# Création et activation d'un utilisateur de base de données dans Database Actions

## Présentation

Cet atelier vous guide tout au long des étapes de prise en main de Database Actions. Vous apprendrez à créer un utilisateur dans Database Actions et à lui donner accès à Database Actions.

Durée estimée : 3 minutes

### Objectifs

*   Découvrez comment configurer les rôles de base de données requis dans Database Actions.
*   Découvrez comment créer un utilisateur de base de données dans Database Actions.

### Prérequis

*   compte cloud Oracle
*   Autonomous Database provisionné

## Tâche 1 : Connexion à Database Actions

Connectez-vous en tant qu'administrateur dans Database Actions de l'instance ADB que vous venez de créer.

Cliquez sur le **menu de navigation** en haut à gauche, accédez à **Oracle Database** et sélectionnez **Autonomous Transaction Processing**.

![base de données-atp](https://oracle-livelabs.github.io/common/images/console/database-atp.png)

Sur la page Détails d'Autonomous Database, ouvrez l'onglet **Outils** et cliquez sur **Database Actions**. Assurez-vous que votre navigateur autorise les fenêtres pop-up.

![console adb](images/adb-console.jpg)

Entrez **ADMIN** en tant que nom utilisateur et passez à la suivante.

![connexion-1](images/login-1.jpg)

Saisissez le mot de passe (que vous avez configuré à l'atelier 2) et connectez-vous.

![connexion-2](images/login-2.jpg)

Accédez au menu **SQL** une fois que vous êtes connecté en tant qu'utilisateur **ADMIN**.

![base de données-actions](images/database-actions.jpg)

## Taks 2 : Créer des rôles de base de données

Créez maintenant les rôles requis pour la fonctionnalité de graphique. Entrez les commandes suivantes dans SQL Worksheet et exécutez-les en étant connecté en tant qu'utilisateur Admin.

    <copy>
    DECLARE
      PRAGMA AUTONOMOUS_TRANSACTION;
      role_exists EXCEPTION;
      PRAGMA EXCEPTION_INIT(role_exists, -01921);
      TYPE graph_roles_table IS TABLE OF VARCHAR2(50);
      graph_roles graph_roles_table;
    BEGIN
      graph_roles := graph_roles_table(
        'GRAPH_DEVELOPER',
        'GRAPH_ADMINISTRATOR',
        'PGX_SESSION_CREATE',
        'PGX_SERVER_GET_INFO',
        'PGX_SERVER_MANAGE',
        'PGX_SESSION_READ_MODEL',
        'PGX_SESSION_MODIFY_MODEL',
        'PGX_SESSION_NEW_GRAPH',
        'PGX_SESSION_GET_PUBLISHED_GRAPH',
        'PGX_SESSION_COMPILE_ALGORITHM',
        'PGX_SESSION_ADD_PUBLISHED_GRAPH');
      FOR elem IN 1 .. graph_roles.count LOOP
      BEGIN
        dbms_output.put_line('create_graph_roles: ' || elem || ': CREATE ROLE ' || graph_roles(elem));
        EXECUTE IMMEDIATE 'CREATE ROLE ' || graph_roles(elem);
      EXCEPTION
        WHEN role_exists THEN
          dbms_output.put_line('create_graph_roles: role already exists. continue');
        WHEN OTHERS THEN
          RAISE;
        END;
      END LOOP;
    EXCEPTION
      when others then
        dbms_output.put_line('create_graph_roles: hit error ');
        raise;
    END;
    /
    </copy>
    

Affectez les droits d'accès par défaut aux rôles, **GRAPH\_ADMINISTRATOR** et **GRAPH\_DEVELOPER**, pour regrouper plusieurs droits d'accès.

    <copy>
    GRANT PGX_SESSION_CREATE TO GRAPH_ADMINISTRATOR;
    GRANT PGX_SERVER_GET_INFO TO GRAPH_ADMINISTRATOR;
    GRANT PGX_SERVER_MANAGE TO GRAPH_ADMINISTRATOR;
    GRANT PGX_SESSION_CREATE TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_NEW_GRAPH TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_GET_PUBLISHED_GRAPH TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_MODIFY_MODEL TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_READ_MODEL TO GRAPH_DEVELOPER;
    </copy>
    

## Tâche 3 : créer un utilisateur de base de données

Créez maintenant l'utilisateur **CUSTOMER\_360** et fournissez l'accès Database Actions à cet utilisateur.

Ouvrez le menu principal et cliquez sur "Database Users".

![utilisateur-1](images/user-1.jpg)

Cliquez sur le bouton **Créer un utilisateur**, entrez le nom utilisateur et le mot de passe. Activez **Web Access** et définissez le quota sur **UNLILMITED**.

![utilisateur-2](images/user-2.png)

Accédez à l'onglet **Rôles accordés** et accordez le rôle **`GRAPH_DEVELOPER`** et le rôle **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** à cet utilisateur. (Deux rôles **CONNECT** et **RESOURCE** sont sélectionnés par défaut. Veuillez les garder cochés pour qu'ils soient également accordés.)

![utilisateur-3](images/user-3.png)

Passez à **Create User** et ouvrez la fenêtre de connexion.

![utilisateur-4](images/user-4.jpg)

Confirmez que vous pouvez vous connecter avec le nouvel utilisateur.

![utilisateur-5](images/user-5.jpg)

Pour plus de détails, reportez-vous à la section sur la [fourniture de l'accès à Database Actions aux utilisateurs de base de données](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/sql-developer-web.html#GUID-4B404CE3-C832-4089-B37A-ADE1036C7EEA) dans la documentation.

Vous pouvez maintenant passer à l'exercice suivant.

## Accusés de réception

*   **Auteur** - Jayant Sharma, chef de produit, Spatial and Graph
*   **Contributeurs** - Arabella Yao, Jenny Tsai
*   **Dernière mise à jour par/date** - Ryota Yamanaka, mars 2023