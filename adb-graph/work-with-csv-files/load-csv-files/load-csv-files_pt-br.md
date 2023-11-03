# Graph Studio: Carregar dados de arquivos CSV em tabelas

## Introdução

Neste laboratório, você carregará dois arquivos CSV em tabelas correspondentes usando a interface do Database Actions da sua instância do Oracle Autonomous Data Warehouse ou do Oracle Autonomous Transaction Processing.

Tempo Estimado: 10 minutos.

Assista ao vídeo abaixo para uma rápida caminhada pelo laboratório.

[](youtube:wkKKO-RO0lA)

### Objetivos

Saiba como

*   carregar arquivos CSV em um Autonomous Database usando o Database Actions

### Pré-requisitos

*   O laboratório a seguir requer uma conta do Oracle Autonomous Database.
*   Presume-se que existe um usuário habilitado para Gráfico e Acesso à Web. Ou seja, existe um usuário do banco de dados com as atribuições e os privilégios corretos e esse usuário pode fazer log-in no Database Actions.

## Tarefa 1: Estabelecer conexão com o Database Actions da instância do Autonomous Database

1.  Abra a página de detalhes do serviço da sua instância do Autonomous Database na Console do Oracle Cloud.
    
    ![O texto ALT não está disponível para esta imagem](images/open-database-actions.png " ")
    
2.  Clique em **Database Actions** para abri-lo.
    

## Tarefa 2: Fazer log-in como o usuário habilitado para gráfico

1.  Faça log-in como o usuário gráfico (por exemplo, `GRAPHUSER`) da sua instância do Autonomous Database.
    
    ![O texto ALT não está disponível para esta imagem](./images/db-actions-graphuser-login.png " ")
    
    > **Observação:** _Se necessário, faça o seguinte para criar o usuário com as funções e privilégios certos_:
    
    *   Faça log-in no Database Actions como o usuário **ADMIN** do seu Autonomous Database
    *   Selecione **Administração** e, em seguida, **Usuários de Banco de Dados** no menu de navegação
    *   Clique em **Criar Usuário**.
    *   Ative os botões **Acesso à Web** e **Gráfico**

## Tarefa 3: Faça download dos conjuntos de dados de amostra do ObjectStore

1.  Copie e cole o url no seu navegador para o arquivo zip, ou seja,
    
        <copy>
        https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
    
    Ou use `wget` ou `curl` para fazer download dos dados de amostra para seu computador.  
    Um exemplo de solicitação `curl` que você pode copiar e colar é:
    
        <copy>
        curl -G -o acct-txn-data.zip https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
2.  **Descompacte** o arquivo em um diretório local, como ~/downloads.
    

## Tarefa 4: Fazer Upload usando o Carregamento de Dados do Database Actions

1.  Clique no cartão **DATA LOAD**.
    
    ![O texto ALT não está disponível para esta imagem](images/db-actions-dataload-card.png " ")
    
    Em seguida, especifique a localização dos seus dados. Ou seja, certifique-se de que as placas **LOAD DATA** e **LOCAL FILE** tenham uma marca de seleção. Clique em **Próximo**.
    
    ![O texto ALT não está disponível para esta imagem](./images/db-actions-dataload-location.png)
    
2.  Clique em **Selecionar Arquivos**.
    
    ![O texto ALT não está disponível para esta imagem](images/db-action-dataload-file-browser.png " ")
    
    Navegue até a pasta correta (por exemplo, ~/downloads/random-acct-data) e selecione os arquivos `bank_accounts.csv` e `bank_txns.csv`.
    
    ![O texto ALT não está disponível para esta imagem](./images/db-actions-dataload-choose-files.png " ")
    
3.  Verifique se os arquivos corretos foram selecionados e clique no ícone **Executar**. ![O texto ALT não está disponível para esta imagem](./images/db-actions-dataload-click-run.png " ")
    
4.  Confirme se você deseja o job de carregamento de dados.
    
    ![O texto ALT não está disponível para esta imagem](./images/db-actions-dataload-confirm-run.png " ")
    
5.  Depois que os arquivos forem carregados
    
    ![O texto ALT não está disponível para esta imagem](./images/dbactions-dataload-files-loaded.png " ")
    
    Clique em **Concluído** para sair.
    
    ![O texto ALT não está disponível para esta imagem](images/dbactions-click-done.png " ")
    
6.  Agora abra a Planilha **SQL**. ![O texto ALT não está disponível para esta imagem](./images/db-actions-choose-sql-card.png " ")
    
7.  Navegue até a pasta correta (por exemplo, ~/downloads) e selecione o arquivo `fixup.sql` e arraste-o para a planilha SQL.
    
    ![O texto ALT não está disponível para esta imagem](./images/db-actions-drag-drop-fixup-sql.png " ")
    
    Se, no entanto, você preferir copiar e colar, o conteúdo de `fixup.sql` será:
    
        <copy>
        alter table bank_accounts add primary key (acct_id);
        
        alter table bank_txns add txn_id number;
        update bank_txns set txn_id = rownum;
        commit;
        
        alter table bank_txns add primary key (txn_id);
        alter table bank_txns modify from_acct_id references bank_accounts (acct_id);
        alter table bank_txns modify to_acct_id references bank_accounts (acct_id);
        
        desc bank_txns;
        
        select * from USER_CONS_COLUMNS where table_name in ('BANK_ACCOUNTS', 'BANK_TXNS');
        </copy>      
        
    
    Faz o seguinte:
    
    *   Adiciona uma restrição de chave primária à tabela `bank_accounts`
    *   Adiciona uma coluna (`txn_id`) à tabela `bank_txns`
    *   Define um valor para `txn_id` e confirma a transação
    *   Adiciona uma restrição de chave primária à tabela `bank_txns`
    *   Adiciona uma restrição de chave estrangeira à tabela `bank_txns` especificando que `from_acct_id` faz referência a `bank_accounts.acct_id`
    *   Adiciona uma segunda restrição de chave estrangeira à tabela `bank_txns` especificando que `to_acct_id` faz referência a `bank_accounts.acct_id`
    *   Ajuda a verificar se a adição de uma coluna `txn_id` e as restrições
8.  Execute o script `fixup.sql` na planilha SQL.  
    ![O texto ALT não está disponível para esta imagem](./images/db-actions-sql-execute-fixup.png " ")
    
9.  A saída do script deve ter a seguinte aparência:
    
    ![O texto ALT não está disponível para esta imagem](./images/db-actions-sql-script-output.png " ")
    
    **Passe para o próximo laboratório** para criar um gráfico a partir dessas tabelas.
    

## Agradecimentos

*   **Autor** - Jayant Sharma, Gerenciamento de Produtos
*   **Colaboradores** - Jayant Sharma, Gerenciamento de Produtos
*   **Última Atualização em/Data** - Jayant Sharma, Gerenciamento de Produtos, fevereiro de 2022