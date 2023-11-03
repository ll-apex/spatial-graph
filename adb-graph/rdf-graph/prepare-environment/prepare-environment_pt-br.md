# Preparar o Ambiente

## Introdução

O Oracle Autonomous Transaction Processing (ATP) é um serviço de banco de dados Oracle totalmente gerenciado com recursos "autônomos" na Oracle Cloud Infrastructure (OCI). É uma prática recomendada criar um usuário com permissões para usar o Graph Studio.

O guia de laboratório a seguir mostra como provisionar um ATP e criar um usuário com permissões para o Graph Studio.

Tempo Estimado: 15 minutos

### Objetivos

*   Crie o Autonomous Database no Oracle Cloud.

### Pré-requisitos

*   Navegador da Web
*   Sempre verifique se você está na Região e no Compartimento corretos

## **Tarefa 1:** Fazer Login no Oracle Cloud

1.  No seu browser, faça log-in no Oracle Cloud.

## **Tarefa 2:** Provisionar ATP

Provisione o banco de dados Autonomous Transaction Processing (ATP) com as etapas a seguir. Como alternativa, um ADW (Autonomous Data Warehouse) pode ser usado de forma semelhante.

1.  Selecione sua Região designada no canto superior direito da console do OCI.
    
2.  No menu de hambúrguer (lado superior esquerdo), selecione Oracle Database e, em seguida, Autonomous Transaction Processing.
    

![Imagem mostrando onde no menu selecionar para acessar o Autonomous Transaction Processing](./images/atp.png)

3.  Clique em Criar Autonomous Database.

![Imagem mostrando o botão para criar um banco de dados autônomo](./images/create-adb.png)

4.  Escolha seu compartimento.
    
5.  Informe qualquer nome exclusivo (talvez seu nome) para o nome de exibição e do banco de dados. O nome para exibição é usado na IU da Console para identificar seu banco de dados.
    

![Imagem mostrando o local para informar um nome exclusivo para o banco de dados](./images/unique-name.png)

6.  Verifique se o tipo de carga de trabalho Processamento de transação está selecionado.
    
7.  Informe uma senha. O nome de usuário é sempre ADMIN. (Observação: lembre-se da sua senha)
    

![Imagem mostrando onde declarar sua senha](./images/password.png)

8.  Clique em Create Autonomous Database na parte inferior.
    
    Seu console mostrará que o ATP está provisionando. Isso levará cerca de 2 ou 3 minutos para ser concluído.
    
    Você pode verificar o status do provisionamento na Solicitação de Serviço.
    

![Imagem mostrando onde verificar o status do banco de dados provisionado](./images/status.png)

Isso conclui este laboratório. _Agora você pode prosseguir para o próximo laboratório._

## Agradecimentos

*   **Autor** - Nicholas Cusato (Santa Monica Specialist Hub)
*   **Colaboradores** - Nicholas Cusato (Santa Monica Specialist Hub)
*   **Última Atualização em/Data** - Nicholas Cusato, fevereiro de 2022