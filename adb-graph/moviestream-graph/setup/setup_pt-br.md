# Configuração: Executar Pilha

## Introdução

Neste laboratório, você criará uma pilha que executará um script terraform para gerar um Autonomous Database, criar um Usuário Gráfico e fazer upload do conjunto de dados que será usado.

Tempo Estimado: 5 minutos.

### Objetivos

Saiba como

*   Execute a pilha para criar um usuário do Autonomous Database, Graph e fazer upload do conjunto de dados
*   Fazer log-in no Graph Studio

## Tarefa 1: Criar compartimento do OCI

[](include:iam-compartment-create-body.md)

## Tarefa 2: Executar Pilha

As instruções abaixo mostrarão como executar uma pilha que criará automaticamente um Autonomous Database contendo um usuário de gráfico e o conjunto de dados necessários para as consultas de gráfico de propriedades.

1.  Faça login no Oracle Cloud.
    
2.  Depois de fazer log-in, use este [link](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://objectstorage.us-ashburn-1.oraclecloud.com/p/0kMdD7Vnv0J1st_2cU-S5PYNWT4SKzOOA04XbhwltUVXnOQ7vec1JJBEGk1eOxPS/n/oradbclouducm/b/moviestream_livelab/o/MovieStream_live_lab_7_AnD.zip) para criar e executar a Pilha.
    

> Observação: o link abrirá uma nova guia ou janela.

3.  Você será direcionado para esta página:

![A página Criar Pilha](./images/create-stack.png)

4.  Marque a caixa "Revi e aceito os Termos de Uso da Oracle" e escolha seu **compartimento**. Deixe o restante como padrão. Clique em **Próximo**.

![Opção para ter verificado e aceitar os Termos de Uso da Oracle](./images/oracle-terms.png)

5.  Selecione o **compartimento** para criar o Autonomous Database e a **região** na qual você está criando a pilha para criar todos os recursos. Clique em **Próximo**. Depois disso, você será levado para a página Verificar, clique em **Criar**.

![A página Criar Pilha](./images/configure-variables.png)

6.  Você será levado para uma página Detalhes do Job com um status inicial mostrado em laranja. O ícone ficará verde depois que o job for concluído com sucesso.
    
    ![O job foi bem-sucedido](./images/successful-job.png)
    

## Agradecimentos

*   **Autor** - Jayant Sharma, Ramu Murakami Gutierrez, Gerenciamento de produtos
*   **Colaboradores** - Rahul Tasker, Jayant Sharma, Ramu Murakami Gutierrez, Gerenciamento de produtos
*   **Última Atualização em/Data** - Ramu Murakami Gutierrez, Gerente de Produtos, fevereiro de 2023