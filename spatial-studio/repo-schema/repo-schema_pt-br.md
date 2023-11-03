# Usuário do Banco de Dados para o Repositório do Spatial Studio

## Introdução

Este laboratório explica a criação do esquema de banco de dados a ser usado para o repositório de metadados do Spatial Studio. Esse é o esquema que armazenará o trabalho que você faz no Spatial Studio, como as definições de Conjuntos de Dados, Análises e Projetos.

O esquema do banco de dados para o repositório do Spatial Studio pode tecnicamente ter qualquer nome. Para consistência com outros workshops do Spatial Studio, nomeamos o nome de usuário **studio\_repo**. Observe que este é um nome de usuário do banco de dados e é distinto dos nomes de usuário do aplicativo Spatial Studio, como o nome de usuário do administrador padrão do Spatial Studio (studio\_admin) criado quando instalamos o próprio aplicativo Spatial Studio.

Tempo de Laboratório Estimado: 5 minutos

### Objetivos

*   Aprender a criar esquema para o repositório de metadados do Spatial Studio
*   Saiba como fazer download da Wallet para conexão com o banco de dados

### Pré-requisitos

*   Uma Conta no Oracle Free Tier, Always Free, Paga ou LiveLabs Cloud
*   Acesso ao banco de dados SQL Developer Web.

## Tarefa 1: Criar Esquema de Recompra

1.  No SQL Developer Web, conecte-se ao banco de dados Autônomo a ser usado para o repositório do Spatial Studio como o usuário **admin**
    
2.  Crie o esquema para o repositório do Spatial Studio. O esquema pode ter qualquer nome, mas para consistência com outros laboratórios, usamos o nome **studio\_repo**. Os requisitos de senha do Oracle Autonomous Database estão [aqui](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/manage-users-create.html#GUID-72DFAF2A-C4C3-4FAC-A75B-846CC6EDBA3F). Anote a senha selecionada, pois a usaremos em etapas posteriores.
    
        <copy>CREATE USER studio_repo
        IDENTIFIED BY <password goes here>;</copy>
        

## Tarefa 2: Atribuir Cota de Tablespace

1.  Designe o tablespace padrão ao esquema do repositório do Spatial Studio. Com o Autonomous Database, você pode usar **dados** de nome de tablespace
    
        <copy>ALTER USER studio_repo
        DEFAULT TABLESPACE data;</copy>
        
2.  Designe cota de tablespace ao esquema do repositório do Spatial Studio. Os metadados do Spatial Studio ocupam uma quantidade muito pequena de armazenamento. Portanto, a cota acomoda principalmente os dados de negócios armazenados no esquema de repositório. Para este laboratório, um valor de cota de **250M** é válido. Você também pode definir o valor como **ilimitado** se for experimentar outros conjuntos de dados.
    
        <copy>ALTER USER studio_repo
        QUOTA <quota value> ON data;</copy>
        

## Tarefa 3: Conceder Permissões

1.  Conceda as seguintes permissões ao usuário do esquema do repositório do Spatial Studio
    
        <copy>
        GRANT CONNECT,
              CREATE SESSION,
              CREATE TABLE,
              CREATE VIEW,
              CREATE SEQUENCE,
              CREATE PROCEDURE,
              CREATE SYNONYM,
              CREATE TYPE,
              CREATE TRIGGER
        TO  studio_repo
        </copy>
        

O esquema studio\_repo agora está pronto para ser usado como repositório do Spatial Studio.

## Tarefa 4: Fazer Download da Wallet

É necessária uma Wallet para que o Spatial Studio estabeleça conexão com o esquema de repositório do Autonomous Database que criamos. Usaremos a Carteira no próximo Laboratório.

1.  Navegue até o seu Autonomous Database e selecione View Details
    
    ![Texto alternativo da imagem](images/repo-schema-1.png "Título da imagem")
    
2.  Selecione a guia Conexão do BD
    
    ![Texto alternativo da imagem](images/repo-schema-2.png "Título da imagem")
    
3.  Clique em Fazer Download da Wallet... ![Texto alternativo da imagem](images/repo-schema-3.png "Título da imagem")
    
    Você será solicitado a informar uma senha para o arquivo Wallet. A Wallet é um único arquivo zip.
    
4.  Salve o arquivo Wallet em um local conveniente. Você precisará desse arquivo no próximo Laboratório.
    

Agora você pode [prosseguir para o próximo laboratório](#next).

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, Database Product Management, março de 2023