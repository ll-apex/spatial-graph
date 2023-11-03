# Acessar o Spatial Studio

## Introdução

Este laboratório explica o processo de acesso ao Oracle Spatial Studio (Spatial Studio) em uma Reserva LiveLabs da Oracle. Seu ambiente inclui o Spatial Studio e um Autonomous Database. No primeiro log-in no Spatial Studio, você fornecerá informações de conexão para seu Autonomous Database.

Tempo de Laboratório Estimado: 10 minutos

### Objetivos

Neste laboratório, você vai:

*   Faça download da Cloud Wallet do seu Autonomous Database
*   Executar log-in pela 1a vez no Spatial Studio fornecendo informações de conexão do Autonomous Database

### Pré-requisitos

*   Uma Reserva LiveLabs concluída para "Introdução ao Oracle Spatial Studio"

## Tarefa 1: Fazer Download da Cloud Wallet do Autonomous Database

1.  Em Detalhes do Workshop, observe seu nome de usuário, senha, Compartimento e endereço IP do Spatial Studio. Em seguida, inicie a Console do Cloud.

![Texto alternativo da imagem](images/1-1.png "Título da imagem")

2.  Acesse usando o **Acesso Direto do Oracle Cloud Infrastructure** usando seu nome de usuário e senha inicial da Nuvem. Será solicitado que você altere a senha padrão.

![Texto alternativo da imagem](images/1-2.png "Título da imagem")

3.  Navegue até o **Oracle Database** e, em seguida, para o **Autonomous Database**.

![Texto alternativo da imagem](images/1-3.png "Título da imagem")

4.  No formulário Compartimento à esquerda, comece a digitar o nome do Compartimento observado anteriormente. Isso filtrará dinamicamente a lista Compartimentos. Uma vez listado, selecione seu Compartimento. Seu Autonomous Database será listado. Clique no link para o seu Autonomous Database.

![Texto alternativo da imagem](images/1-4.png "Título da imagem")

5.  Clique em **Conexão do Banco de Dados** e em **Fazer Download da Wallet**. Você será promovido para uma senha da wallet. Informe qualquer string, pois essa senha não será usada. Salve a carteira em um local conveniente em seu laptop, pois você a usará na próxima etapa.

![Texto alternativo da imagem](images/1-5.png "Título da imagem")

## Tarefa 2: Log-in pela Primeira Vez do Spatial Studio

1.  Agora você usará o endereço IP do Spatial Studio que anotou anteriormente. Abra uma nova aba no navegador e navegue até **https://\[seu endereço IP do Spatial Studio\]:4040/spatialstudio**. Por exemplo, se seu endereço IP do Spatial Studio for 123.123.12.123, navegue até https://123.123.12.123:4040/spatialstudio. Como sua instância do Spatial Studio não está configurada com um certificado SSL assinado, você verá uma advertência de segurança específica do browser. Aceite o aviso e prossiga para o site. Em um ambiente de produção, um certificado seria configurado e isso não ocorreria. Faça login com o usuário **admin** e a senha **welcome1**.

![Texto alternativo da imagem](images/2-1.png "Título da imagem")

2.  O log-in pela primeira vez no Spatial Studio solicita que você insira informações de conexão do banco de dados para o repositório de metadados do Spatial Studio. Clique em **Autonomous Database** e em **Próximo**. Na próxima scren, arraste e solte o arquivo de wallet baixado anteriormente e clique em **Ok**.

![Texto alternativo da imagem](images/2-2.png "Título da imagem")

3.  Agora você será solicitado a fornecer informações de conexão do Banco de Dados Automático. Informe o usuário **studio\_repo**, a senha **Welcome1Welcome1** e selecione o nível de serviço médio.

![Texto alternativo da imagem](images/2-3.png "Título da imagem")

O Spatial Studio agora está criando suas tabelas de metadados no Autonomous Database. Isso levará cerca de 30 segundos.

4.  Quando o Spatial Studio abre, o login pela primeira vez é concluído e você está pronto para continuar com o workshop.

![Texto alternativo da imagem](images/2-4.png "Título da imagem")

Agora você pode [prosseguir para o próximo laboratório](#next).

## Saiba Mais

*   [Página do produto Spatial Studio](https://oracle.com/goto/spatialstudio)

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management
*   **Última Atualização em/Data** - David Lapp, Database Product Management, junho de 2021