# Introdução

## Sobre este Workshop

Neste workshop, você provisionará o Spatial Studio para o Oracle Cloud no OCI Cloud Marketplace e preparará um esquema no Autonomous Database para ser usado como repositório de metadados do Spatial Studio.

Tempo de Oficina Estimado: 60 minutos

### Sobre o Oracle Spatial Studio

O Oracle Spatial Studio (Spatial Studio) é um aplicativo web que oferece acesso de autoatendimento aos recursos espaciais do Oracle Database. Embora esses recursos tenham exigido historicamente a codificação e/ou o uso de ferramentas de 3a parte, o Spatial Studio permite que os usuários corporativos criem e compartilhem análises espaciais e mapas da web interativos usando GUIs de autoatendimento.

![Texto alternativo da imagem](./images/spatial-studio.png "Estúdio espacial")

O Spatial Studio opera em dados espaciais no Oracle Database, o que significa tabelas e views que incluem o tipo de dados de geometria da Oracle. Estes dados são dados espaciais pré-existentes ou dados não espaciais que são preparados usando o Spatial Studio para adicionar geometrias com base em atributos.

O Spatial Studio é um aplicativo Java EE que pode ser implantado no Oracle Cloud no Oracle Cloud Marketplace. O Spatial Studio também pode ser implantado manualmente no Oracle WebLogic ou Jetty ou como um Início Rápido pré-implantado para teste.

Para mais informações, visite \[https://oracle.com/goto/spatialstudio\] (https://oracle.com/goto/spatialstudio)

### Objetivos

*   Aprender a criar e designar um esquema de banco de dados para o repositório de metadados do Spatial Studio
*   Saiba como usar o Cloud Marketplace para instalar o Spatial Studio
*   Saiba como desinstalar o Spatial Studio quando não for mais necessário

### Pré-requisitos

*   Este workshop requer um Oracle Autonomous Database.
*   O SQL Developer Web é fornecido com o Autonomous Database e também é usado para criar o esquema de repositório do Spatial Studio.
*   Se você já tiver acesso a eles, seguindo esta Introdução, poderá pular para o Laboratório 3.
*   Caso contrário, você deve prosseguir para o Laboratório 1.
*   Nenhuma experiência anterior com o Oracle Spatial é necessária.
*   Uma Conta do Oracle Cloud - Exiba a página de destino LiveLabs deste workshop para ver quais ambientes são suportados

_Observação: Se você tiver uma conta de **Avaliação Gratuita**, quando sua Avaliação Gratuita expirar, sua conta será convertida em uma conta **Always Free**. Você não poderá realizar workshops sobre Free Tier a menos que o ambiente Always Free esteja disponível. **[Clique aqui para ver a página de Perguntas Frequentes sobre o Free Tier.](https://www.oracle.com/cloud/free/faq.html)**_

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, Database Product Management, janeiro de 2021