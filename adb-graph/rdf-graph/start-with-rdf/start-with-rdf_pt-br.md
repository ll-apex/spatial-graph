# Conceitos Básicos de Gráficos RDF

## Introdução

Este laboratório apresenta as etapas para começar a fazer upload dos dados RDF para um bucket que será vinculado ao Autonomous Database. Isso requer a cópia do nome de usuário correto do OCI do perfil. Para permitir que o Graph Studio acesse os dados RDF no OCI Object Storage (usando o pacote DBMS\_CLOUD), crie um token de acesso usando sua conta do OCI. Isso será usado no laboratório secundário.

Tempo Estimado: 5 minutos

### Objetivos

*   Fazer Upload de Dados RDF no OCI Object Storage
*   Exibir seu Nome de Usuário do OCI
*   Gerar token de Acesso

### Pré-requisitos

Este laboratório pressupõe que você tenha:

*   Conta do Oracle Cloud
*   Faça download do arquivo MOVIESTREAM (moviestream\_rdf.nt) usando este [link](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)

## **Tarefa 1:** Fazer Upload de Dados RDF para o OCI Object Storage

1.  Acesse a console do OCI usando suas credenciais do Oracle Cloud.
2.  Abra o menu de navegação e clique em Armazenamento. Em Object Storage & Archive Storage, clique em Buckets, conforme mostrado: ![Imagem que descreve onde a pasta buckets é selecionada no menu](./images/buckets-folder.png)
3.  Selecione um Compartimento que se aplique à sua conta do OCI. ![Imagem mostrando onde o menu drop-down Compartimento está na página Buckets](./images/compartment-menu.png)
4.  Clique em Create Bucket. O controle deslizante Criar Bucket é aberto conforme mostrado: ![Imagem descrevendo a página Criar Bucket](./images/create-bucket.png)
5.  Informe o Nome do Bucket, deixe todo o resto como padrão e clique em Create. O bucket é criado e listado na página Buckets, conforme mostrado: ![Imagem mostrando o resultado da criação de um Bucket](./images/bucket-result.png)
6.  Clique no link RDF\_DATA\_BUCKET e navegue até a página Detalhes do Bucket.

![Imagem mostrando a página Bucket após a criação](./images/bucket-page.png) 7. Clique em Upload na seção Objetos. O controle deslizante Fazer Upload de Objetos é aberto. 8. Selecione o arquivo RDF moviestream\_rdf.nt baixado [link](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt) no sistema local e clique em Upload. O upload do arquivo foi bem-sucedido. Clique em Fechar para retornar à página Detalhes do Período. O arquivo carregado é listado em Objects conforme mostrado: ![Imagem mostrando o objeto carregado no Bucket](./images/image-upload.png)

1.  Selecione o menu Ações do arquivo submetido a upload e clique em Exibir Detalhes do Objeto para acessar as propriedades do arquivo submetido a upload. O controle deslizante Object Details é aberto conforme mostrado: ![Imagem mostrando o Menu Objeto exibido destacando a opção Exibir Detalhes do Objeto](./images/object-details.png)
2.  Observe o caminho do URL do objeto. Isso é usado no assistente de importação RDF no Graph Studio. ![Imagem mostrando onde encontrar o caminho do URL para o objeto no Bucket](./images/url-path.png)

## **Tarefa 2:** Exibir seu Nome de Usuário do OCI

1.  Clique no ícone do avatar no canto superior direito para abrir seu perfil. A primeira entrada em Perfil é seu nome de usuário do OCI. ![Imagem mostrando como acessar o perfil do OCI](./images/oci-profile.png)
2.  Observe seu nome de usuário do OCI. Isso é usado no assistente de importação RDF no Graph Studio. ![Imagem mostrando o nome de usuário do OCI em Detalhes do Usuário](./images/oci-username.png)

## **Tarefa 3:** Gerar um Token de Acesso na Console do OCI

1.  Acesse a console do OCI usando suas credenciais do Oracle Cloud.
    
2.  Clique no ícone de avatar no canto superior direito para abrir seu perfil e clique em Configurações do usuário. ![Imagem mostrando como acessar as Configurações do Usuário no perfil](./images/user-settings.png)
    
3.  Clique em Tokens de Autenticação em Recursos, conforme mostrado: ![Imagem mostrando como acessar Tokens de Autenticação no menu Recursos das Definições do Usuário](./images/auth-tokens.png)
    
4.  Clique em Gerar Token. A caixa de diálogo Gerar Token é aberta. ![Imagem mostrando como gerar um Token de Autenticação](./images/gen-tokens.png)
    
5.  Informe uma Descrição e clique em Gerar Token. Os detalhes do Token Gerado são exibidos conforme mostrado: ![Imagem mostrando como copiar o Token de Autenticação gerado](./images/token-details.png)
    
6.  Clique em Copiar para copiar o token e salvá-lo para uso posterior.
    

Isso conclui este laboratório. _Agora você pode prosseguir para o próximo laboratório._

## Agradecimentos

*   **Autor**\- Melliyal Annamalai, Gerente Distinto de Produtos
*   **Contribuidor Técnico** - Nicholas Cusato, Santa Monica Specialist Hub
*   **Última Atualização em/Data** - Nicholas Cusato, Santa Monica Specialist Hub, 25 de fevereiro de 2022