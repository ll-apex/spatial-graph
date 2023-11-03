# Instalar o Spatial Studio

## Introdução

Este laboratório explica o processo de provisionamento do Oracle Spatial Studio (Spatial Studio) usando o Oracle Cloud Marketplace. O Oracle Cloud Marketplace fornece aplicativos e serviços fornecidos pela Oracle e 3 partes. Os detalhes estão disponíveis [aqui](https://docs.oracle.com/en/cloud/marketplace/marketplace-cloud/index.html).

Tempo de Laboratório Estimado: 30 minutos

### Objetivos

Neste laboratório, você vai:

*   Saiba como instalar o Spatial Studio no Oracle Cloud Marketplace
*   Saiba como definir o esquema do repositório do Spatial Studio na inicialização inicial

### Pré-requisitos

*   Uma Conta no Oracle Free Tier, Always Free, Paga ou LiveLabs Cloud
*   Esquema de repositório criado (Laboratório 3).

## Tarefa 1: Selecionar Spatial Studio no Marketplace

1.  Clique no **Menu de Navegação** no canto superior esquerdo e selecione **Marketplace**.

![Oracle Cloud Marketplace](https://oracle-livelabs.github.io/common/images/console/marketplace.png "Mercado")

2.  Procure o Spatial Studio e clique no aplicativo Oracle Spatial Studio

![Oracle Spatial Studio no Oracle Cloud Marketplace](images/env-marketplace-2.png "Imagens do Oracle Spatial Studio Marketplace")

3.  Revise as Instruções de Uso, aceite os termos e condições e clique em Iniciar Pilha

![Iniciar pilha para implantar o Oracle Spatial Studio](images/env-marketplace-3.png "Iniciar Pilha")

## Tarefa 2: Assistente de Criação de Pilha

1.  Opcionalmente, informe um nome e uma descrição personalizados para a pilha de implantação. Em seguida, selecione o Compartimento a ser usado para a implantação e clique em Next

![Criar assistente de pilha](images/env-marketplace-4.png "Criar a pilha usando o assistente")

2.  Selecione o Domínio de Disponibilidade e a Forma da Instância de Computação.

Os detalhes sobre formas de computação estão [aqui](https://docs.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm). Verifique a disponibilidade de cota da Forma desejada nos Domínios de Disponibilidade. Isso é particularmente importante ao usar uma forma Always Free: \*Na Console do OCI, navegue até Governança > Limites, Cotas e Uso \* Para Serviço, selecione Computação e para Escopo, selecione um Domínio de Disponibilidade \*Confirme a disponibilidade da Forma desejada \* Altere a seleção do Domínio de Disponibilidade, se necessário, para identificar a cota disponível

![Limites, cotas e uso de recursos do Oracle Cloud](images/env-marketplace-4-1.png "Limite para recursos de Computação")

Após confirmar a cota, faça seleções no assistente Criar Pilha.

![Definir parâmetros de pilha](images/env-marketplace-5.png "Selecionar instância de computação")

Em seguida, role para baixo.

3.  Opcionalmente, altere a porta HTTPS e o nome de usuário administrador do Spatial Studio dos padrões. Para a autenticação do usuário administrador do Spatial Studio, você tem a opção de usar Segredos do OCI Vault ou uma senha. A imagem abaixo mostra um exemplo usando uma senha. Para implantações de produção, recomendamos que você use os Segredos do OCI Vault. Role para baixo até a seção sobre configuração de rede.

Observação: Por padrão, o nome de usuário administrador do Spatial Studio é **admin**. Este é um usuário do aplicativo Spatial Studio distinto do nome de usuário do banco de dados (studio\_repo) criado no Laboratório 3 para o esquema de repositório armazenado no banco de dados.

![Definir mais parâmetros, como porta e senha](images/env-marketplace-6.png "Configuração Avançada do Spatial Studio - Senha do usuário administrador do Spatial Studio")

4.  Para rede, você tem a opção de criar automaticamente uma nova VCN ou uma existente. Selecione o Compartimento para criar uma nova VCN ou procurar VCNs existentes.

A imagem abaixo mostra um exemplo usando Criar Nova VCN. Para usar uma VCN existente, ela deve estar no mesmo Domínio de Disponibilidade selecionado acima na Etapa 2. Se você não tiver outras VCNs existentes, os padrões restantes poderão ser deixados como estão. Se você tiver outras VCNs existentes, atualize os valores de CIDR para evitar conflitos.

![Configurar a rede](images/env-marketplace-7.png "Configuração Avançada do Spatial Studio - Configuração de rede")

Role para baixo até a seção Chaves SSH.

5.  O carregamento de uma chave pública SSH permite o acesso ao sistema de arquivos do Spatial Studio para fins administrativos. A caixa de diálogo tem links para a documentação geral de conexão SSH. Envie sua chave pública SSH navegando até o arquivo de chaves ou copiando a string de chaves. Se você carregar a chave pública SSH de um arquivo, o nome do arquivo da chave será exibido conforme mostrado na imagem abaixo. Clique em Próximo.

![Adicionar chave SSH](images/env-marketplace-8.png "Configuração Avançada do Spatial Studio - Chave SSH Pública")

6.  Revise o resumo de suas entradas. Se forem necessárias correções, clique em Voltar. Caso contrário, clique em Criar para iniciar o processo de implantação. Você será redirecionado para uma página Detalhes do Job da implantação.

![Criar pilha](images/env-marketplace-9.png "Revise a definição da pilha e crie a pilha")

## Tarefa 3: Monitorar o Andamento da Implantação

1.  A seção Logs na parte inferior da página Detalhes do Job mostrará o andamento. Inicialmente, ele exibirá um spinner durante a configuração para implantação.

![Monitorar job de implantação de pilha - Aplicação do Terraform](images/env-marketplace-10.png "Monitore o progresso da implantação da pilha")

Após alguns minutos, você verá informações de log.

![Informações de log sobre o job de implantação](images/env-marketplace-11.png "Log de implantação da pilha")

2.  Role para baixo até a parte inferior da seção de logs. Quando concluído, você verá Aplicar Completo! seguido pelos detalhes da instância. O último item listado é o URL público do Spatial Studio. Copie este URL e cole em um browser.

![Job de implantação concluído com sucesso](images/env-marketplace-12.png "Variáveis de saída para a pilha implantada")

## Tarefa 4: Log-in pela Primeira Vez

1.  Abrir o URL público do Spatial Studio pela primeira vez exibirá um aviso do navegador relacionado à privacidade e segurança. O aviso específico depende da sua plataforma e navegador.

![Advertência ao abrir o URL do Spatial Studio](images/env-marketplace-13.png "Advertência da conexão do browser")

Este não é um problema do Spatial Studio; é genérico para acessar sites que não têm um certificado HTTPS assinado. O carregamento e a configuração de um certificado assinado remove este aviso. No entanto, o processo de carregamento de certificados na Jetty está além do escopo deste workshop.

Clique no link para continuar no site.

2.  Informe o nome de usuário administrador do Spatial Studio (o padrão é admin) e a senha informada na Etapa 2 (assistente de Criação de Pilha, item 3). Em seguida, clique em Sign In.

![Forneça nome de usuário e senha para fazer log-in no Spatial Studio](images/env-marketplace-14.png "Caixa de diálogo de login do Spatial Studio")

3.  No primeiro log-in em uma instância do Spatial Studio, você será solicitado a fornecer informações de conexão para que o esquema do banco de dados seja usado como repositório de metadados do Spatial Studio. Este é o esquema de banco de dados usado para todos os metadados do Spatial Studio e também pode ser usado por usuários administradores do Spatial Studio para armazenar outros dados. Você usará o esquema criado no Laboratório 3. Portanto, selecione Oracle Autonomous Database e clique em Próximo.

![Escolher tipo de conexão de metadados](images/env-marketplace-15.png "Escolher o tipo de repositório de metadados do Spatial Studio")

4.  Navegue até (ou arraste e solte) o arquivo Wallet salvo no Laboratório 3. Após o carregamento, o nome do arquivo da wallet será listado como Wallet Selecionada. Clique em OK.

![Fazer upload da wallet](images/env-marketplace-16.png "Faça upload da wallet de conexão")

5.  Insira o nome de usuário e a senha definidos no Laboratório 2 e no serviço. O nível médio de serviço é apropriado para este workshop. Clique em OK.

![Informe os detalhes da conexão para o repositório de metadados](images/env-marketplace-17.png "Informar detalhes da conexão")

6.  Aguarde alguns instantes enquanto o Spatial Studio estabelece sua conexão inicial com o esquema e cria várias tabelas de metadados. Quando terminar, o Spatial Studio abrirá com informações de Conceitos Básicos.

![Página inicial do Spatial Studio - Introdução](images/env-marketplace-18.png "Página inicial do Spatial Studio")

## Tarefa 5: Carregar Dados e Criar um Mapa

Para verificar se o Spatial Studio está funcionando corretamente, você carregará, preparará e visualizará uma pequena amostra de dados. Os dados contêm uma lista de museus, incluindo nome e endereço. Você geocodificará os dados e visualizará os dados em um mapa interativo.

1.  Você não criará uma conexão aqui, pois pode usar a conexão do repositório do Spatial Studio para esta verificação. Clique no mosaico para **Criar Conjunto de Dados**.

![Iniciar assistente para fazer upload de dados](images/verify-1.png "Criar um conjunto de dados")

2.  Faça download do arquivo de amostra de dados [aqui](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/sf_area_museums.xlsx) e salve no local conveniente. Em seguida, arraste e solte o arquivo no bloco de upload do arquivo. Você também pode clicar no bloco de upload de arquivo e navegar até o arquivo.

![Criar um conjunto de dados fazendo upload dos dados](images/verify-2.png "Carregar dados existentes da planilha")

3.  Na visualização de dados, defina a Conexão de upload como SPATIAL\_STUDIO e defina o tipo de dados POSTAL\_CODE como STRING. Em seguida, clique em **Enviar**.

![Especificar detalhes de upload](images/verify-3.png "Especificar detalhes de upload e verificar definições de coluna")

4.  Quando o upload for concluído, o conjunto de dados será listado com um ícone de aviso indicando que as ações precisam ser executadas. Clique no ícone de aviso e, em seguida, clique no link **Ir para Colunas do Conjunto de Dados** para designar uma coluna de chave.

![Definir a coluna de chave para o conjunto de dados](images/verify-4.png "Resolver problemas do conjunto de dados - escolher ou adicionar coluna-chave")

5.  Selecione NAME como a chave e clique em **Validar chave**.

![Validar chave](images/verify-5.png "Validar a chave escolhida")

Depois de validar a chave, clique em **Aplicar**.

6.  Clique novamente no ícone de aviso e, em seguida, clique no botão para **Endereços do Código Geográfico** para converter endereços em locais de coordenadas para visualização do mapa.

![Endereços de código geográfico](images/verify-7.png "Resolver problemas do conjunto de dados - endereços de código geográfico")

7.  Observe que as colunas ADDRESS e POSTAL\_CODE foram detectadas automaticamente para uso em geocodificação. Aceite os padrões e clique em **Aplicar**.

![Mapeamento de endereços de código geográfico](images/verify-8.png "Mapear conjunto de dados com dados de referência de geocodificação")

Quando a geocodificação estiver concluída, você retornará à página Conjuntos de Dados.

8.  Clique no menu de ação do conjunto de dados SF\_AREA\_MUSEUMS e selecione **Criar Projeto**.

![Começar a criar o projeto](images/verify-9.png "Crie um novo projeto para o conjunto de dados")

9.  Clique e arraste o conjunto de dados SF\_AREA\_MUSEUMS e solte em qualquer lugar do mapa.

![Adicionando conjuntos de dados e arraste-os para a tela do mapa](images/verify-10.png "Adicionar conjuntos de dados como camadas ao projeto")

O conjunto de dados SF\_AREA\_MUSEUMS será adicionado como uma camada de mapa e o mapa panorâmico e ampliará a área dos dados.

10.  Clique no menu de ação da camada SF\_AREA\_MUSEUMS e selecione **Definições**

![Definições de camada de dados](images/verify-11.png "Defina estilos e muito mais para a camada de dados")

11.  Estilize a camada do mapa selecionando uma cor e opacidade de sua escolha.

![Definição de estilo](images/verify-12.png "Selecionar cor e opacidade da camada de dados")

12.  Clique na guia **Interação**, ative a **janela Mostrar informações** e selecione todas as colunas. Em seguida, clique em um item no mapa para ver uma janela de informações com os valores de dados do item selecionado.

![Configurações para interações do mapa](images/verify-13.png "Definir detalhes para interagir com o mapa")

Isso verifica se a preparação e a visualização de dados básicos estão funcionando corretamente.

13\. Clique no botão do painel de navegação esquerdo para retornar à página Conjuntos de Dados. Selecione a opção **Descartar Alterações**, pois não é necessário preservar esse teste.

![Descartar alterações](images/verify-14.png "Descartar as alterações feitas no projeto atual")

14.  Com a verificação concluída, você pode excluir o Conjunto de Dados de teste e a tabela de banco de dados. Clique no menu de ação de SF\_AREA\_MUSEUMS e selecione **Excluir**

![Excluir conjunto de dados](images/verify-15.png "Excluir o conjunto de dados")

15.  Selecione a opção para excluir a tabela de banco de dados e clique em **OK**.

![Marque para excluir permanentemente a tabela de banco de dados](images/verify-16.png "Excluir a tabela do banco de dados relacionada ao conjunto de dados")

O Oracle Spatial Studio agora é provisionado e testado. O Laboratório a seguir fornece etapas para derrubar o Spatial Studio quando não for mais necessário.

## Tarefa 6: Desinstalar o Spatial Studio (quando não for mais necessário)

**Se você deseja remover completamente sua implantação do Marketplace, prossiga com o seguinte.**

1.  Clique no **Menu de Navegação** no canto superior esquerdo, navegue até **Serviços do Desenvolvedor** e selecione **Pilhas**.

![Limpar todos os recursos implantados](https://oracle-livelabs.github.io/common/images/console/developer-resmgr-stacks.png "Remover a implantação do Marketplace")

2.  Escolha o Compartimento e o Nome usados na PASSO 2. No exemplo mostrado abaixo, um compartimento chamado sandbox e Stack chamado Oracle Spatial Studio foi usado.

![Escolha o compartimento adequado e selecione a pilha a ser excluída](images/env-marketplace-20.png "Selecionar pilha")

3.  Selecione Ações do Terraform > Destruir

![Destrua todos os recursos implantados por meio da pilha do Oracle Spatial Studio](images/env-marketplace-21.png "Destruir recursos implantados")

Você será solicitado a confirmar. Isso removerá os artefatos de Computação e Rede criados pela implantação do Marketplace.

4.  Após remover o aplicativo Spatial Studio, seu esquema de repositório permanece no local. Para remover o esquema do repositório, conecte-se ao banco de dados como **admin** como feito no Laboratório 3 e execute o seguinte.

    <copy>DROP USER studio_repo CASCADE;</copy>
    

## Saiba Mais

*   [Página do produto Spatial Studio](https://www.oracle.com/database/spatial/#rc30p2)
*   [Introdução ao Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, Database Product Management, março de 2023