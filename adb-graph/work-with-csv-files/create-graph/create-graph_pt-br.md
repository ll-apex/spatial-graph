# Graph Studio: Criar um gráfico usando a instrução PGQL CREATE PROPERTY GRAPH

## Introdução

Neste laboratório, você criará um gráfico das tabelas `bank_accounts` e `bank_txns` usando o Graph Studio e a instrução CREATE PROPERTY GRAPH.

Tempo Estimado: 15 minutos.

Assista ao vídeo abaixo para uma rápida apresentação do laboratório. [Passo a Passo](videohub:1_jguolqf3)

### Objetivos

Saiba como

*   usar o Graph Studio e o PGQL DDL (ou seja, a instrução CREATE PROPERTY GRAPH) para modelar e criar um gráfico com base em tabelas ou views existentes.

### Pré-requisitos

*   O laboratório a seguir requer um Autonomous Database - Serverless.
*   E que o usuário habilitado para Gráfico (`GRAPHUSER`) existe. Ou seja, existe um usuário de banco de dados com as atribuições e os privilégios corretos.

## Tarefa 1: Acessar o Autonomous Database

1.  Clique no **Menu de Navegação** no canto superior esquerdo, navegue até o **Oracle Database** e selecione **Autonomous Database**.
    
    ![Navegando até o Autonomous Database.](images/navigation-menu.png " ")
    
2.  Selecione o compartimento fornecido em **Exibir Informações de Log-in** e clique no **Nome para Exibição** do **Autonomous Database**.
    
    ![Selecionando o Autonomous Database no Menu de Navegação.](images/select-autonomous-database.png " ")
    

## Tarefa 2: Fazer Log-in no Graph Studio

O Graph Studio é um recurso do Autonomous Database. Ele está disponível como uma opção no Launchpad do Database Actions. Você precisa de um usuário habilitado para gráfico para fazer log-in no Graph Studio. Este usuário já foi criado para você.

1.  Na página **Detalhes do Autonomous Database**, clique no botão **Database Actions** e selecione **Exibir todas as ações do banco de dados**.
    
    ![Clique no botão Database Actions](images/click-database-actions.png " ")
    
2.  No painel Database Actions, clique em **Graph Studio**.
    
    ![Clique em Open Graph Studio](images/graphstudiofixed.png " ")
    
3.  Faça logon no Graph Studio. Use as credenciais do usuário do banco de dados GRAPHUSER.
    
    ![Use as credenciais do usuário do banco de dados MOVIESTREAM](images/graph-login.png " ")
    
    O Graph Studio consiste em um conjunto de páginas acessadas no menu à esquerda.
    
    O ícone **Home** leva você para a Home page.  
    A página **Gráfico** lista gráficos existentes para uso em notebooks.  
    A página **Notebook** lista notebooks existentes e permite criar um novo.  
    A página **Modelos** permite que você crie modelos para as visualizações de gráfico.  
    A página **Jobs** lista o status dos jobs em segundo plano e permite exibir o log associado, se houver.  
    

## Tarefa 3: Criar um gráfico de contas e transações

1.  Clique no ícone **Gráfico**. Em seguida, clique em **Criar Gráfico**.
    
    ![Mostra onde está o modelador de botão de criação](images/graph-create-button.png " ")
    
2.  Informe `bank_graph` como o nome do gráfico e clique em **próximo**. Os campos de descrição e tags são opcionais.  
    Esse nome de gráfico é usado no próximo laboratório.  
    Não informe outro nome porque as consultas e os trechos de código no próximo laboratório falharão.
    
    ![Mostra a janela criar gráfico na qual você atribui um nome ao gráfico](./images/create-graph-dialog.png " ")
    
3.  Expanda **GRAPHUSER** e selecione as tabelas `BANK_ACCOUNTS` e `BANK_TXNS`.
    
    ![Mostra como selecionar BANK_ACCOUNTS e BANK_TXNS](./images/select-tables.png " ")
    
4.  Mova-os para a direita, ou seja, clique no primeiro ícone no controle de transporte.
    
    ![Mostra as tabelas selecionadas](./images/selected-tables.png " ")
    
5.  Clique em **Próximo**. Vamos editar e atualizar este gráfico para adicionar uma borda e um rótulo de vértice.
    
    O gráfico sugerido tem `BANK_ACCOUNTS` como uma tabela de vértices, pois há restrições de chave estrangeira especificadas em `BANK_TXNS` que fazem referência a ele.
    
    E `BANK_TXNS` é uma tabela de borda sugerida.
    
    ![Mostra a tabela de vértices e bordas](./images/create-graph-suggested-model.png " ")
    
6.  Agora vamos alterar os rótulos Vertex e Edge padrão.
    
    Clique na tabela de vértices `BANK_ACCOUNTS`. Altere o Rótulo Vertex para **ACCOUNTS**. Em seguida, clique na marca de seleção para confirmar o rótulo e salvar a atualização.
    
    ![Alterado o nome do label do vértice para Contas](images/edit-accounts-vertex-label.png " ")
    
    Clique na tabela de borda `BANK_TXNS` e renomeie o Label de Borda de `BANK_TXNS` para **TRANSFERS**. Em seguida, clique na marca de seleção para confirmar o rótulo e salvar a atualização.
    
    ![Alterou o nome do rótulo da borda para Transferências](images/edit-edge-label.png " ")
    
    Isso é **importante** porque usaremos esses rótulos de borda no próximo laboratório deste workshop ao consultar o gráfico. Clique em **Próximo**.
    

7.  Na etapa Resumo, clique em **Criar Gráfico**.
    
    ![Mostra a guia do job com o status de job como bem-sucedido](./images/jobs-create-graph.png " ")
    
    Isso abrirá uma guia Criar Gráfico, clique em **Criar Gráfico**.
    
    ![Mostra na memória ativado e o botão criar gráfico](./images/create-graph-in-memory.png " ")
    
    Depois disso, você será levado à página Jobs, na qual o gráfico será criado.
    
    Isso conclui este laboratório. **Agora você pode prosseguir para o próximo laboratório.**
    

## Agradecimentos

*   **Autor** - Jayant Sharma, Gerenciamento de Produtos
*   **Colaboradores** - Jayant Sharma, Gerenciamento de Produtos
*   **Última Atualização em/Data** - Ramu Murakami Gutierrez, Gerente de Produtos, junho de 2023