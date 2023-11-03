# Criar o Usuário do Graph

## Introdução

Neste laboratório, você criará um usuário de banco de dados com as atribuições e os privilégios apropriados necessários para usar os recursos gráficos do Autonomous Database.

Tempo Estimado: 5 minutos.

Assista ao vídeo abaixo para uma rápida caminhada pelo laboratório.

[Link para o vídeo deste workshop](youtube:CQh8Q24Rboc)

### Objetivos

Saiba como

*   criar um usuário do banco de dados com as atribuições e privilégios apropriados necessários para acessar o **Graph Studio**

### Pré-requisitos

*   O laboratório a seguir requer uma conta do Autonomous Data Warehouse - Shared Infrastructure ou do Autonomous Transaction Processing - Shared Infrastructure

## Tarefa 1: Estabelecer conexão com o Database Actions da instância do Autonomous Database

1.  Abra a página de detalhes do serviço da sua instância do Autonomous Database na console do OCI.
    
    Em seguida, clique no link **Database Actions** para abri-lo.
    
    ![Home page do Autonomous Database apontando para o botão Database Actions](images/open-database-actions.png "Home page do Autonomous Database apontando para o botão Database Actions")
    

## Tarefa 2: Criar o acesso à Web e o usuário habilitado para gráfico

1.  Faça log-in como o usuário ADMIN da sua instância do Autonomous Database.
    
    ![Faça log-in na sua instância do Autonomous Database](./images/login.png "Faça log-in na sua instância do Autonomous Database")
    
2.  Clique no mosaico **USUÁRIOS DE BANCO DE DADOS** em **Administração**.
    
    ![Clique no mosaico do Database Actions](./images/db-actions-users.png "Clique no mosaico do Database Actions")
    
3.  Clique no ícone **\+ Criar Usuário**.
    
    ![Clique em Create User](./images/db-actions-create-user.png "Clique em Create User ")
    
4.  Informe os detalhes necessários, ou seja, nome de usuário e senha. Ative os botões de opção **Ativar Gráfico** e **Acesso à Web**. E selecione uma cota, por exemplo, **UNLIMITED**, para alocar no tablespace `DATA`.
    
    Observação: A senha deve atender aos seguintes requisitos:
    
    *   A senha deve ter de 12 a 30 caracteres e deve incluir pelo menos uma letra alta, uma letra baixa e um caractere numérico.
    *   A senha não pode conter o nome de usuário.
    *   A senha não pode conter o caractere de aspas duplas (").
    *   A senha deve ser diferente das 4 últimas senhas usadas para este usuário.
    *   A senha não deve ser a mesma que foi definida há menos de 24 horas.
    
    ![Defina o nome de usuário e a senha do Gráfico e selecione Criar Usuário](images/db-actions-create-graph-user.png "Defina o nome de usuário e a senha do Gráfico e selecione Criar Usuário ")
    
    **Observação: Não Ative o Gráfico para o usuário ADMIN e não faça log-in no Graph Studio como o usuário ADMIN. O usuário ADMIN tem privilégios adicionais por padrão. Crie e use uma conta com apenas os privilégios necessários com dados gráficos e análises.**
    
    Clique no botão **Criar Usuário** na parte inferior do painel para criar o usuário com as credenciais especificadas.
    
    O usuário recém-criado será listado.
    
    ![O usuário recém-criado será listado](./images/db-actions-user-created.png "O usuário recém-criado será listado ")
    
    **Observação:** _As etapas da IU acima podem ser executadas executando os seguintes comandos sql listados abaixo quando conectado como ADMIN. Portanto, o Passo 5 abaixo não é necessário. Ela mostra uma maneira alternativa de criar e ativar o GRAPHUSER._
    
5.  Aloque uma cota de espaço de tabela desejada para o usuário recém-criado. Abra a página SQL e execute o comando alter.
    
    Por exemplo, `ALTER USER GRAPHUSER QUOTA UNLIMITED ON DATA;`  
    alocará uma cota para o usuário `GRAPHUSER` no tablespace chamado `DATA`.  
    Copie e cole o comando a seguir na planilha SQL.  
    Substitua os valores corretos para `<username>` e `<quota>` e clique em Run para executá-los.
    
        <copy>
        -- Optional statement to use in place of the UI of the Administration page
        ALTER USER <username> QUOTA <quota> ON DATA;
        </copy>
        
    
        <copy>
        -- Optional statements to use in place of the UI of the Administration page
        GRANT GRAPH_DEVELOPER TO <username> ;
        ALTER USER <username> GRANT CONNECT THROUGH "GRAPH$PROXY_USER";
        </copy>
        
    
    As capturas de tela abaixo mostram um exemplo de execução da instrução ALTER USER.
    
    ![Alterar cota de usuário para 10G](./images/alter-user.png "Alterar cota de usuário para 10G")
    
    ![Executar a instrução alter user](./images/run-sql.png "Executar a instrução alter user")
    
    ![O usuário será exibido como alterado na saída do script](./images/user-altered.png "O usuário será exibido como alterado na saída do script")
    
6.  Da mesma forma, você pode usar instruções SQL para verificar se o GRAPHUSER foi configurado corretamente.
    
    Você deve fazer log-in no SQL de Ações de Dados como `ADMIN`, informar as instruções SQL a seguir e executá-las.
    
        <copy>
        select * from dba_role_privs where grantee='GRAPHUSER';
        
        select * from dba_proxies where client='GRAPHUSER';
        </copy>
        
    
    Os resultados devem ser os mesmos que nas capturas de tela abaixo.
    
    ![Concede atribuições e privilégios ao usuário do gráfico](images/graphuser-role-privs.png "Concede atribuições e privilégios ao usuário do gráfico")
    
    ![Conceder proxy ao usuário do gráfico](images/graphuser-proxy-grant.png "Conceder proxy ao usuário do gráfico")
    

**Passe para o próximo laboratório** para saber como criar e analisar gráficos no ADB.

## Agradecimentos

*   **Autor** - Jayant Sharma, Gerenciamento de Produtos
*   **Colaboradores** - Korbi Schmid, Rahul Tasker
*   **Última Atualização em/Data** - Jayant Sharma, junho de 2023