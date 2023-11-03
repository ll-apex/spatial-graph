# Criar e Ativar um Usuário de Banco de Dados no Database Actions

## Introdução

Este laboratório apresenta as etapas para começar a usar o Database Actions. Você aprenderá a criar um usuário no Database Actions e a fornecer a esse usuário o acesso ao Database Actions.

Tempo estimado: 3 minutos

### Objetivos

*   Saiba como configurar as atribuições de banco de dados necessárias no Database Actions.
*   Saiba como criar um usuário de banco de dados no Database Actions.

### Pré-requisitos

*   Conta do Oracle Cloud
*   Autonomous Database Provisionado

## Tarefa 1: Fazer Login no Database Actions

Faça log-in como o usuário Admin no Database Actions da instância do ADB recém-criada.

Clique no **Menu de Navegação** na parte superior esquerda, navegue até o **Oracle Database** e selecione **Autonomous Transaction Processing**.

![atp do banco de dados](https://oracle-livelabs.github.io/common/images/console/database-atp.png)

Na página Detalhes do Autonomous Database, abra a guia **Ferramentas** e clique em **Database Actions**. Certifique-se de que seu brower permita janelas pop-up.

![adb-console](images/adb-console.jpg)

Digite **ADMIN** como Nome do Usuário e vá em seguida.

![login-1](images/login-1.jpg)

Insira a senha (configurada no Laboratório 2) e efetue sign-in.

![login-2](images/login-2.jpg)

Vá para o menu **SQL** depois de fazer log-in como o usuário **ADMIN**.

![ações do banco de dados](images/database-actions.jpg)

## Taks 2: Criar atribuições de banco de dados

Agora crie as funções necessárias para o recurso de gráfico. Informe os comandos a seguir na Planilha SQL e execute-a enquanto estiver conectado como o usuário Admin.

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
    

Designe as permissões padrão às atribuições, **GRAPH\_ADMINISTRATOR** e **GRAPH\_DEVELOPER**, para agrupar várias permissões.

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
    

## Tarefa 3: Criar um usuário do banco de dados

Agora crie o usuário **CUSTOMER\_360** e forneça acesso ao Database Actions para esse usuário.

Abra o menu principal e clique em "Usuários do Banco de Dados".

![usuário-1](images/user-1.jpg)

Clique no botão **Criar Usuário**, insira o nome de usuário e a senha. Ative o **Acesso à Web** e defina a cota como **UNLILMITED**.

![usuário-2](images/user-2.png)

Vá para a guia **Atribuições Concedidas** e conceda a atribuição **`GRAPH_DEVELOPER`** e a atribuição **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** a este usuário. (Duas atribuições **CONNECT** e **RESOURCE** são selecionadas por padrão. Por favor, mantenha-os verificados para que eles também sejam concedidos.)

![usuário-3](images/user-3.png)

Prossiga com **Criar Usuário** e abra a janela de log-in.

![usuário-4](images/user-4.jpg)

Confirme se você pode fazer log-in com o novo usuário.

![usuário-5](images/user-5.jpg)

Para obter detalhes, consulte a seção ["Fornecer aos Usuários de Banco de Dados Acesso ao Database Actions"](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/sql-developer-web.html#GUID-4B404CE3-C832-4089-B37A-ADE1036C7EEA) na documentação.

Agora você pode ir para o próximo laboratório.

## Agradecimentos

*   **Autor** - Jayant Sharma, Gerente de Produtos, Espacial e Gráfico
*   **Colaboradores** - Arabella Yao, Jenny Tsai
*   **Última Atualização em/Data** - Ryota Yamanaka, março de 2023