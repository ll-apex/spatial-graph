# Introdução

## Sobre este Workshop

Neste workshop, você explorará o mapeamento no Oracle APEX usando o recurso Map Region e o Oracle Spatial. Você instalará e explorará um aplicativo de amostra pré-criado com muitos exemplos de mapeamento úteis. Em seguida, você criará seu próprio aplicativo e configurará mapas usando um assistente e do zero.

A Região do Mapa é um recurso nativo do APEX introduzido no APEX 21.1, fornecendo a capacidade de configurar mapas interativos que exibem dados espaciais do Oracle Spatial, GeoJSON e coordenadas. Este workshop se concentra em usar o Oracle Spatial como fonte de dados espaciais, para que os dados espaciais brutos e os resultados da análise espacial sejam facilmente incorporados.

![Aplicativo de Mapas de Amostra](./images/intro-01.png "Oracle Application Express - Aplicativo de Mapas de Amostra ")

Tempo de Oficina Estimado: 1 hora e 15 minutos

### Sobre o Oracle Application Express (APEX) e o Oracle Spatial

O Oracle Application Express (APEX) e o Oracle Spatial são recursos do Oracle Database, incluindo os serviços Autonomous Data Warehouse (ADW) e Autonomous Transaction Processing (ATP).

O Oracle Application Express (APEX) é uma plataforma de desenvolvimento de baixo código que permite criar aplicativos empresariais escaláveis e seguros com recursos de excelência mundial. Além disso, é possível implantá-lo em qualquer ambiente. Mais informações na [página inicial do Oracle APEX Product](https://apex.oracle.com)

O Oracle Spatial é um conjunto de recursos de gerenciamento, análise e processamento de dados geoespaciais no Oracle Database. Com um tipo de dados espaciais nativos e operações de análise, a análise baseada em localização é mainstream e co-localizada com todas as outras operações de banco de dados. Mais na [página inicial do Produto Oracle Spatial](https://www.oracle.com/database/spatial)

### Objetivos

*   Compreender amostras da Região do Mapa do APEX
*   Aprenda a criar e configurar a Região do Mapa
*   Aprenda a incorporar a análise de localização com o Oracle Spatial

### Pré-requisitos

*   O Oracle APEX 21.1+ é obrigatório. as capturas de tela neste workshop serão feitas usando o APEX 21.2. Como geralmente recomendamos o uso da [versão mais recente do APEX](https://www.oracle.com/tools/downloads/apex-downloads/), espere pequenas diferenças ocasionais na interface do usuário.
*   A experiência básica com o Oracle APEX é recomendada, embora não seja necessária. Se necessário, revise o seguinte workshop introdutório do LiveLabs APEX: [Criando um Aplicativo com base em Tabelas Existentes para o Oracle Autonomous Cloud Service](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=628).
*   A experiência básica com o Oracle Spatial é recomendada, embora não seja necessária. Se necessário, analise o seguinte workshop introdutório LiveLabs Spatial: [Introdução ao Oracle Spatial](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=736)

_Observação: Se você tiver uma conta de **Avaliação Gratuita**, quando sua Avaliação Gratuita expirar, sua conta será convertida em uma conta **Always Free**. Você não poderá realizar workshops sobre Free Tier a menos que o ambiente Always Free esteja disponível. **[Clique aqui para ver a página de Perguntas Frequentes sobre o Free Tier.](https://www.oracle.com/cloud/free/faq.html)**_

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Colaboradores** - Jayson Hanes, APEX Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, março de 2023