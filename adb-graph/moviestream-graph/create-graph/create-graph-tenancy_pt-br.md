# Criar um Gráfico

## Introdução

Neste laboratório, você criará um gráfico das tabelas `MOVIE, CUSTOMER\_SAMPLE` e `WATCHED` usando a experiência do usuário guiada do Graph Studio.

Tempo Estimado: 15 minutos.

### Objetivos

Saiba como

*   usar o Graph Studio para modelar e criar um gráfico com base em tabelas ou views existentes.

### Pré-requisitos

*   O laboratório a seguir requer uma instância sem Servidor do Autonomous Database.
*   E que o usuário habilitado para Gráfico existe. Ou seja, existe um usuário de banco de dados com as atribuições e os privilégios corretos.

## Tarefa 1: Acessar o Autonomous Database

1.  Clique no **Menu de Navegação** no canto superior esquerdo, navegue até o **Oracle Database** e selecione **Autonomous Database**.
    
    ![Navegando até o Autonomous Database.](images/navigation-menu.png " ")
    
2.  Selecione seu **compartimento** e clique no **Nome para Exibição** do **Autonomous Database**.
    
    ![Selecionando o Autonomous Database no Menu de Navegação.](images/select-autonomous-database.png " ")
    

## Tarefa 2: Fazer Log-in no Graph Studio

[](include:adb-goto-graph-studio.md)

## Tarefa 3: Criar um gráfico de Recomendações de Filme

[](include:adb-create-graph.md)

## Agradecimentos

*   **Autor** - Melli Annamalai, Gerente de Produtos, Oracle Spatial and Graph
*   **Colaboradores** - Jayant Sharma
*   **Última Atualização em/Data** - Ramu Murakami Gutierrez, Gerente de Produtos, Oracle Spatial and Graph, julho de 2023