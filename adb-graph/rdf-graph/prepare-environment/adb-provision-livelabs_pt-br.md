/\* EXCLUIR ESTE ARQUIVO NA PRÓXIMA VERSÃO - USE ADB-PROVISION-CONDITIONAL.MD FILE INSTEAD E ESPECIFIQUE A VERSÃO QUE VOCÊ QUER EM SEU MANIFESTO: { "title": "Lab 1: Provision an ADB Instance", "description": "Provisioning an Autonomous Database Instance", "type": "livelabs", "filename": "https://oracle-livelabs.github.io/adb/shared/adb-provision/adb-provision-conditional.md" }, \*/

# Provisionar um Autonomous Database (ADW e ATP)

## Introdução

Este laboratório apresenta as etapas para começar a usar o Oracle Autonomous Database (Autonomous Data Warehouse \[ADW\] e o Autonomous Transaction Processing \[ATP\]) no Oracle Cloud. Neste laboratório, você provisiona uma nova instância do ADW.

> **Observação:** enquanto este laboratório usa o ADW, as etapas são idênticas para criar um banco de dados ATP.

Tempo estimado: 5 minutos

### Objetivos

*   Saiba como provisionar um novo Autonomous Database

## Tarefa 1: Escolhendo ADW ou ATP no Menu Serviços

1.  Faça login no Oracle Cloud.
    
2.  Depois de fazer log-in, você será levado ao painel de serviços de nuvem, onde poderá ver todos os serviços disponíveis para você. Clique no menu de navegação no canto superior esquerdo para mostrar as opções de navegação de nível superior.
    
    > **Observação:** você também pode acessar diretamente seu serviço Autonomous Data Warehouse ou Autonomous Transaction Processing na seção **Ações Rápidas** do painel de controle.
    
    ![Home page da Oracle.](./images/Picture100-36.png " ")
    
3.  As etapas a seguir se aplicam de forma semelhante ao Autonomous Data Warehouse ou ao Autonomous Transaction Processing. Este laboratório mostra o provisionamento de um banco de dados Autonomous Data Warehouse; portanto, clique em **Autonomous Data Warehouse**.
    
    ![Clique em Autonomous Data Warehouse.](https://oracle-livelabs.github.io/common/images/console/database-adw.png " ")
    
4.  Certifique-se de que seu tipo de carga de trabalho seja **Data Warehouse** ou **Tudo** para ver suas instâncias do Autonomous Data Warehouse. Use o menu drop-down **Escopo da Lista** para selecionar um compartimento. Informe a primeira parte do seu nome de usuário, por exemplo, `LL185` no campo Pesquisar Compartimentos para localizar rapidamente seu compartimento.
    
    ![Verifique o tipo de carga de trabalho à esquerda.](images/livelabs-compartment.png " ")
    
5.  Essa console mostra que ainda não existem bancos de dados. Se houvesse uma longa lista de bancos de dados, você poderia filtrar a lista pelo **Estado** dos bancos de dados (Disponível, Interrompido, Encerrado etc.). Você também pode classificar por **Tipo de Carga de Trabalho**. Aqui, o tipo de carga de trabalho **Data Warehouse** é selecionado.
    
    ![Console de Autonomous Databases.](./images/Compartment.png " ")
    

## Tarefa 2: Criando a instância do ADB

1.  Clique em **Create Autonomous Database** para iniciar o processo de criação de instâncias.
    
    ![Clique em Criar Autonomous Database.](./images/Picture100-23.png " ")
    
2.  Isso ativa a tela **Create Autonomous Database**, na qual você especificará a configuração da instância.
    
    ![](./images/create-adb-screen-livelabs-default.png " ")
    
3.  Forneça informações básicas para o banco de dados autônomo:
    
    *   **Escolher um compartimento** - Deixe o compartimento padrão.
    *   **Display Name** - Digite um nome memorável para o banco de dados para fins de exibição. Para este laboratório, use **ADW Finance Mart**.
    *   **Nome do Banco de Dados** - Use apenas letras e números, começando com uma letra. O tamanho máximo é de 14 caracteres. (Subnúcleos não suportados inicialmente.) Para este laboratório, use **ADWFINANCE** e **anexe seu id de usuário**. Por exemplo, se seu id de usuário for **LL-185**, digite **ADWFINANCE185**
    
    ![Informe os detalhes necessários.](./images/Picture100-26-livelabs.png " ")
    
4.  Escolha um tipo de carga de trabalho. Selecione o tipo de carga de trabalho para seu banco de dados entre as opções:
    
    *   **Data Warehouse** - Para este laboratório, escolha **Data Warehouse** como o tipo de carga de trabalho.
    *   **Processamento de Transação** - Como alternativa, você poderia ter escolhido Processamento de Transação como o tipo de carga de trabalho.
    
    ![Escolha um tipo de carga de trabalho.](./images/Picture100-26b.png " ")
    
5.  Escolha um tipo de implantação. Selecione o tipo de implantação para seu banco de dados entre as opções:
    
    *   **Shared Infrastructure** - Para este laboratório, escolha **Shared Infrastructure** como o tipo de implantação.
    *   **Infraestrutura Dedicada** - Como alternativa, você poderia ter escolhido Infraestrutura Dedicada como o tipo de implantação.
    
    ![Escolha um tipo de implantação.](./images/Picture100-26_deployment_type.png " ")
    
6.  Configure o banco de dados:
    
    *   **Always Free** - Se sua Conta do Cloud for uma conta Always Free, você poderá selecionar esta opção para criar um banco de dados autônomo sempre gratuito. Um banco de dados sempre gratuito vem com 1 CPU e 20 GB de armazenamento. Para este laboratório, recomendamos que você deixe a opção Always Free desmarcada.
    *   **hoose database version** - Selecione uma versão do banco de dados entre as versões disponíveis.
    *   **Contagem de OCPUs** - Número de CPUs do seu serviço. Para este laboratório, especifique **1 CPU**. Se você escolher um banco de dados Always Free, ele virá com 1 CPU.
    *   **Storage (TB)** - Selecione sua capacidade de armazenamento em terabytes. Para este laboratório, especifique **1 TB** de armazenamento. Ou, se você escolher um banco de dados Always Free, ele virá com 20 GB de armazenamento.
    *   **Dimensionamento Automático** - Para este laboratório, mantenha o dimensionamento automático ativado, para permitir que o sistema use automaticamente até três vezes mais recursos de CPU e Entrada/Saída para atender à demanda da carga de trabalho.
    *   **New Database Preview** - Se uma caixa de seleção estiver disponível para visualizar uma nova versão do banco de dados, NÃO selecione-a.
    
    > **Observação:** Não é possível ampliar/ reduzir um banco de dados autônomo Always Free.
    
    ![Escolha os parâmetros restantes.](./images/Picture100-26c.png " ")
    
7.  Crie credenciais de administrador:
    
    *   **Password and Confirm Password** - Especifique a senha para o usuário ADMIN da instância de serviço. A senha deve atender aos seguintes requisitos:
    *   A senha deve ter de 12 a 30 caracteres e deve incluir pelo menos uma letra alta, uma letra baixa e um caractere numérico.
    *   A senha não pode conter o nome de usuário.
    *   A senha não pode conter o caractere de aspas duplas (").
    *   A senha deve ser diferente das 4 últimas senhas usadas.
    *   A senha não deve ser a mesma que foi definida há menos de 24 horas.
    *   Digite novamente a senha para confirmá-la. Anote essa senha.
    
    ![Informe a senha e confirme-a.](./images/Picture100-26d.png " ")
    
8.  Escolha o acesso à rede:
    
    *   Para este laboratório, aceite o padrão, "Acesso seguro de todos os lugares".
    *   Se você quiser permitir o tráfego apenas dos endereços IP e VCNs especificados - em que o acesso ao banco de dados de todos os IPs ou VCNs públicos é bloqueado, selecione "Proteger o acesso de IPs e VCNs permitidos apenas" na área Escolher acesso à rede.
    *   Se você quiser restringir o acesso a um ponto final privado dentro de uma VCN do OCI, selecione "Private endpoint access only" na área Choose network access.
    *   Se a opção "Require mutual TLS (mTLS) authentication" estiver selecionada, será necessário o mTLS para autenticar conexões com o seu Autonomous Database. As conexões TLS permitem que você estabeleça conexão com seu Autonomous Database sem uma wallet, se você usar um driver thin JDBC com JDK8 ou superior. Consulte a [documentação para opções de rede](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/support-tls-mtls-authentication.html#GUID-3F3F1FA4-DD7D-4211-A1D3-A74ED35C0AF5) para obter opções para permitir TLS ou para exigir apenas autenticação mTLS (TLS mútuo).
    
    ![Escolha o acesso à rede.](./images/Picture100-26e.png " ")
    
9.  Escolha um tipo de licença. Para este laboratório, escolha **BYOL (Bring Your Own License)**. Os dois tipos de licença são:
    
    *   **BYOL (Bring Your Own License)** - Selecione este tipo quando a sua organização tiver licenças de banco de dados existentes.
    *   **License Included** - Selecione este tipo quando quiser assinar novas licenças de software de banco de dados e o serviço de nuvem de banco de dados.
    
    ![Clique em Criar Autonomous Database.](./images/Picture100-27-byol.png " ")
    
10.  Para este laboratório, não forneça um endereço de e-mail de contato. O campo "Contact Email" permite listar contatos para receber avisos operacionais e anúncios, bem como notificações de manutenção não programada.
    
    ![Não forneça um endereço de e-mail de contato.](images/contact-email-field.png)
    
11.  Clique em **Criar Autonomous Database**.
    
12.  Sua instância começará a provisionar. Em alguns minutos, o estado passará de Provisionamento para Disponível. Nesse momento, seu banco de dados Autonomous Data Warehouse está pronto para uso! Dê uma olhada nos detalhes da sua instância aqui, incluindo nome, versão do banco de dados, contagem de OCPUs e tamanho do armazenamento.
    

    ![Database instance homepage.](./images/Picture100-32.png " ")
    

_Passe para o próximo laboratório_.

## Quer saber mais?

Clique [aqui](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3) para obter documentação sobre o workflow típico para usar o Autonomous Data Warehouse.

## Agradecimentos

*   **Autor** - Nilay Panchal, Gerenciamento de Produtos ADB
*   **Adaptado para Nuvem por** - Richard Green, Desenvolvedor Principal, Assistência ao Usuário do Banco de Dados
*   **Colaboradores** - Equipe de QA do Oracle LiveLabs (Jeffrey Malcolm Jr, Estagiário | Arabella Yao, Gerente de Produtos Estagiário)
*   **Última Atualização em/Data** - Richard Green, fevereiro de 2022