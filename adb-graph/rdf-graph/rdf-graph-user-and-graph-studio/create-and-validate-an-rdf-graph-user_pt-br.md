# Criar e Validar um Usuário de Gráfico RDF no Graph Studio

## Introdução

Neste laboratório, criaremos e validaremos um Usuário do Gráfico RDF no Graph Studio.

Tempo Estimado: 10 minutos

### Objetivos

*   Criar um Usuário do Gráfico para Acessar o RDF no Graph Studio
*   Ativar RDF para o Usuário do Gráfico
*   Criar Gráfico RDF no Graph Studio
*   Validar o Gráfico RDF
*   Executar Consultas SPARQL na Página Playground

### Pré-requisitos

Este laboratório pressupõe que você tenha:

*   Uma Conta no Oracle Free Tier ou Paga no Cloud
*   Você concluiu:
    *   Laboratório 1: Provisionar uma Instância do ADB

## Tarefa 1: Criar um usuário do gráfico para acessar o RDF no Graph Studio

Para trabalhar com Gráficos RDF no Graph Studio, você deve criar usuários de gráficos com atribuições concedidas. Você pode criar usuários do Graph com o conjunto correto de atribuições e privilégios usando o Oracle Database Actions.

Navegue até a sua instância do Autonomous Database e crie um usuário do gráfico seguindo as etapas abaixo ou conforme explicado em [Criar um Usuário do Gráfico](https://docs.oracle.com/en/cloud/paas/autonomous-database/csgru/create-graph-user.html)

1.  Navegue até o seu Autonomous Database e clique no nome para exibição do seu banco de dados para exibir seus detalhes.

![A tela do Oracle Cloud Autonomous Database destacando o botão de ações do banco de dados](./images/autonomous-database.png)

2.  Abra o **Database Actions** na barra de ferramentas.

![A tela do Oracle Cloud Autonomous Database mostrando o Autonomous Database for Graph Studio.](./images/adb-details.png)

3.  No Launchpad do Database Actions, clique em **Usuários de Banco de Dados** em **Administração**.

![A tela do inicializador de ações do banco de dados, destacando a página de usuários do banco de dados sob administração](./images/database-actions-launchpad.png)

4.  Clique em **Criar Usuário** na página Usuários da Banco de Dados na área **Todos os Usuários**.

![A página de usuários do banco de dados destacando o botão 'criar usuário'](./images/database-users.png)

5.  Digite um nome de usuário e uma senha.

Observação: A senha deve atender aos seguintes requisitos:

*   A senha deve ter de 12 a 30 caracteres e deve incluir pelo menos uma letra alta, uma letra baixa e um caractere numérico.
    
*   A senha não pode conter o nome de usuário.
    
*   A senha não pode conter o caractere de aspas duplas (").
    
*   A senha deve ser diferente das 4 últimas senhas usadas para este usuário.
    
*   A senha não deve ser a mesma que foi definida há menos de 24 horas.
    

**Por exemplo:** Password12345#

_Anote ou salve seu nome de usuário e senha, pois isso será necessário em um exercício posterior._

![A página de criação de usuário mostrando a seção de criação de nome de usuário e senha, uma cota ilimitada no tablespace DATA e recursos de acesso gráfico e web ativados](./images/create-user.png)

6.  Ativar **gráfico**
    
7.  Ative o **Acesso à Web** e expanda os Recursos Avançados de Acesso à Web, certifique-se de que a autorização seja obrigatória, seu nome de usuário seja igual ao seu Alias REST e o Tipo de Mapeamento de URL seja BASE\_PATH.
    
8.  Defina a **Cota no Tablespace DATA** como Ilimitada.
    
9.  Clique em **Criar Usuário**.
    
    Agora você poderá ver seu usuário criado na seção **Todos os Usuários** da página **Usuários do Banco de Dados** ou ao procurar seu usuário.
    

![A página de usuários do banco de dados mostrando o usuário do banco de dados criado acessível em 'todos os usuários'](./images/graph-user-created.png)

## Tarefa 2: Criar gráfico RDF no Graph Studio

Para que possamos criar um gráfico RDF, primeiro devemos importar dados RDF para o Graph Studio.

1.  Na página **Detalhes do Autonomous Database**, clique no **Database Actions**.

![Clique no botão Database Actions](images/click-database-actions.png " ")

2.  No painel Database Actions, clique em **Graph Studio**.

![Clique em Open Graph Studio](images/graph-studio-fixed.png " ")

3.  Faça logon no Graph Studio. Use as credenciais do usuário do banco de dados MOVIESTREAM.

![Use as credenciais do usuário do banco de dados MOVIESTREAM](images/graph-login.png " ")

4.  Clique em Gráficos no menu de navegação à esquerda para navegar na página Gráficos.

![A página 'começar' do Graph Studio. Na barra de navegação à esquerda, o botão 'Gráficos' é destacado](./images/graph-studio-home.png)

5.  Selecione **RDF GRAPH** como o tipo de gráfico e clique em **Criar Gráfico**.

![O menu suspenso do tipo de gráfico da página do Graph Studio exibe as opções de gráfico PG e RDF](./images/graph-studio-graphs.png)

Em seguida, na janela pop-up, selecione **Gráfico RDF** e clique em **Confirmar**.

![Janelas pop-up solicitando a seleção de gráficos ou coleções rdf](./images/select-rdf-graph.png)

6.  O Assistente de criação de gráfico RDF é aberto conforme mostrado:

![A página 'criar gráfico RDF'.](./images/create-rdf-graph.png)

7.  Informe o caminho do URI do OCI Object Storage:
    
          <copy>https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt
        
8.  Clique em **Nenhuma Credencial**.
    
9.  Clique em **Próximo**. A caixa de diálogo a seguir deve aparecer, digite "MOVIESTREAM" para o Nome do Gráfico:
    

![A segunda página 'criar gráfico RDF'](./images/create-rdf-graph-2.png)

10.  Clique em **Criar**.
    
    O job de criação do gráfico RDF será iniciado. Como o arquivo RDF contém registros 139461, o processo pode levar de 3 a 4 minutos. Você pode monitorar o job na página **Jobs** no Graph Studio.
    

![A página 'jobs' do Graph Studio exibe um job 'Criar um Gráfico RDF - MOVIESTREAM' ainda em andamento](./images/graph-studio-jobs.png)

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
    

## Tarefa 3: Validar o gráfico RDF

Você pode explorar e validar o gráfico RDF recém-criado na página **Gráficos** no Graph Studio, conforme mostrado:

1.  Navegue até a página **Gráficos** e defina o **Tipo de Gráfico** como RDF usando o menu suspenso. Selecione a linha do gráfico MOVIESTREAM entre os gráficos RDF disponíveis, exemplos de instruções (triplos ou quads devem aparecer), use os três pontos horizontais para redimensionar essas instruções e exibi-las. As instruções de amostra (triplos ou quádruplos) do Gráfico RDF são exibidas no painel inferior, conforme mostrado:

![As instruções de amostra do gráfico RDF 'MOVIESTREAM' são exibidas em trigêmeos](./images/graph-sample-statements.png)

## Tarefa 4: Executar consultas SPARQL na página de playground

Você pode executar Consultas SPARQL no Gráfico RDF na página **Plano de Reprodução da Consulta**.

1.  Na página **Gráficos**, selecione o **RDF** no menu drop-down Tipo de Gráfico e clique no botão **Consultar** para navegar até a página Playground da Consulta.

![Página Gráficos com o tipo de gráfico RDF selecionado e o botão de consulta destacado](./images/graph-type.png)

2.  Se você tiver vários gráficos no Graph Studio, terá que escolher o gráfico a ser consultado. No menu Nome do Gráfico, selecione MOVIESTREAM no menu suspenso.

![O playground de consulta exibe o nome do gráfico 'MOVIESTREAM' selecionado no menu suspenso](./images/query-playground.png)

3.  Execute a consulta a seguir para o Gráfico RDF.
    
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
        
    
    Quando a consulta for executada com sucesso, a saída da consulta será exibida conforme mostrado:
    

![O playground de consulta exibe a execução bem-sucedida de uma consulta no gráfico RDF MOVIESTREAM e exibe os resultados da consulta](./images/query-playground-script.png)

Isso conclui este laboratório. _Agora você pode prosseguir para o próximo laboratório._

## Agradecimentos

*   **Autor** - Malia German, Ethan Shmargad, Matthew McDaniel Engenheiros de Soluções, Gerente de Produtos Ramu Murakami Gutierrez
*   **Contribuinte Técnico** - Melliyal Annamalai Gerente de Produto, Joao Paiva Consulting Membro da Equipe Técnica, Lavanya Jayapalan Principal User Assistance Developer
*   **Última Atualização em/Data** - Gerente de Produtos Ramu Murakami Gutierrez, junho de 2023