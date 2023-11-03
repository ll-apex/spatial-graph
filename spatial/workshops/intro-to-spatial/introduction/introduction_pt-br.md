# Introdução

## Sobre o Oracle Spatial

A missão da Oracle é ajudar as pessoas a ver os dados de novas maneiras, descobrir insights e desbloquear infinitas possibilidades. A análise espacial é sobre a compreensão de interações complexas com base em relações geográficas - respondendo a perguntas com base em onde as pessoas, ativos e recursos estão localizados. Os insights espaciais permitem que você ofereça um melhor atendimento ao cliente, otimize sua força de trabalho, localize centros de varejo e distribuição, avalie campanhas de vendas e marketing e muito mais. Com as ofertas espaciais da Oracle, desenvolvedores, profissionais de banco de dados e analistas podem usar um conjunto abrangente de ferramentas de gerenciamento, análise e visualização de dados espaciais para integrar análise espacial e mapeamento a aplicações em infraestrutura de gerenciamento de dados de nível empresarial - Oracle Database e Oracle Exadata. Tecnologias inovadoras da Oracle Cloud e do Oracle Autonomous Database, o único banco de dados independente, autoprotegido e autorreparável do setor, estão disponíveis para aplicações espaciais.

Conforme ilustrado abaixo, os recursos espaciais do Oracle Database fornecem armazenamento, processamento e análise escaláveis e de alto desempenho de tipos de dados espaciais básicos e avançados. Uma série de componentes Java EE implantáveis também é fornecida para suportar serviços comuns de camada intermediária.

![texto alternativo de imagem](./images/spatial-platform.png)

Para mais informações, visite \[https://oracle.com/goto/spatial\] (https://oracle.com/goto/spatial)

Tempo de Oficina Estimado: 60 minutos

### Visão geral do workshop

Neste workshop, você criará, configurará e analisará dados espaciais. Você criará e configurará tabelas espaciais para STORES, WAREHOUSES, REGIONS e TORNADO\_PATHS a partir de formatos comuns e, em seguida, executará consultas espaciais para explorar seus relacionamentos com base na proximidade e na contenção. Você finalmente transforma os resultados usando suporte JSON nativo no ADB, para integração do desenvolvedor.

A capacidade de relacionar informações com base na localização, como relacionar dados com base na proximidade espacial e contenção, é extremamente valiosa em inúmeros cenários. Não há chave preexistente que relaciona os locais da loja a um depósito. Mas o Spatial permite que esse relacionamento seja determinado com base na proximidade. Da mesma forma, não há relacionamento pré-existente entre locais e regiões da loja, por exemplo, regiões de imposto. Mas o Spatial permite que seu relacionamento seja determinado com base na contenção. Indo além, o Spatial permite análises baseadas em localização, como resumir informações com base na proximidade; por exemplo, perda devido a tornados a uma distância de um local. Em vez de executar essas análises em um sistema separado, você pode aproveitar os recursos espaciais incorporados do ADB.

Você ganhará experiência com todas as capacidades acima mencionadas neste workshop.

### Pré-requisitos

\- Uma Conta do Oracle Cloud \- Este workshop requer acesso a um cliente Oracle Database e SQL (ou seja, SQL Developer, SQL Developer Web, SQL\*Plus). - Se você já tiver acesso a eles, após esta Introdução, poderá pular para a seção Criar Dados de Amostra. - Caso contrário, deverá prosseguir para as seções Oracle Cloud Account, Autonomous Database e SQL Developer Web. - Não é necessária experiência anterior com o Oracle Spatial. - Uma Conta do Oracle Cloud

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Colaboradores** - Karin Patenge, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, setembro de 2022