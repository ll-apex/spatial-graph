# Trabalhar com o Graph Studio

## Sobre Este Workshop

Este workshop apresenta os principais conceitos de análise e modelagem de dados gráficos usando os recursos do Graph Studio em um Autonomous Database. Ele mostra como usar consultas de gráfico para encontrar pagamentos circulares que podem indicar transações fraudulentas e algoritmos de análise de gráfico para identificar contas pelas quais muitas transações fluem. Você consultará dados contendo contas (artificiais) e informações de transações. Você começará criando um gráfico, consultando o gráfico, executando um algoritmo de análise e visualizando os resultados. Uma seção opcional apresenta conceitos de gráficos semânticos (RDF), comumente usados para Gráficos de Conhecimento, e mostra como carregar dados de um formato de gráfico RDF padrão, como o formato n-triplo, e como consultá-lo usando SPARQL, a linguagem de consulta para gráficos RDF.

Tempo de Oficina Estimado: 75 minutos

Se quiser assistir ao workshop, clique [aqui](https://youtu.be/Ymk9TE9Q2K4).

### Sobre o Graph Studio

O Oracle Autonomous Database tem recursos que permitem que ele funcione como um banco de dados gráfico escalável. Eles automatizam a criação de modelos gráficos e gráficos na memória com base em tabelas de banco de dados. Eles incluem notebooks e APIs do desenvolvedor para executar consultas gráficas usando PGQL, uma linguagem de consulta gráfica semelhante a SQL, mais de 60 algoritmos gráficos incorporados usando APIs Java ou Python e visualização gráfica nativa.

Assista aos dois vídeos a seguir para obter mais informações sobre o Graph Studio. A primeira é uma introdução aos gráficos de propriedades e seus casos de uso. O segundo é um tour pela interface do Graph Studio.

[Simplificar Análises Gráficos com o Autonomous Database](youtube:eCd-969hrak) Simplificar Análises Gráficos com o Autonomous Database

[Autonomous Database: Um tour pela interface do Graph Studio](youtube:S6Q-IJcBkU0) Autonomous Database: Um tour pela interface do Graph Studio

### Objetivos

Neste workshop, você irá:

*   Criar um gráfico usando a instrução CREATE PROPERTY GRAPH de PGQL (uma linguagem de consulta de gráfico)
*   Carregar o gráfico na memória para análise
*   Criar um notebook
*   Consultar e visualizar o gráfico usando parágrafos de notebook PGQL
*   Execute algoritmos de gráfico e visualize os resultados

### Pré-requisitos

*   Conta do Oracle Cloud
*   Autonomous Database Provisionado - Instância sem Servidor

Isso conclui este laboratório. **Agora você pode prosseguir para o próximo laboratório.**

## Agradecimentos

*   **Autor** - Jayant Sharma, Gerenciamento de Produtos
*   **Colaboradores** - Jayant Sharma, Gerenciamento de Produtos
*   **Última Atualização em/Data** - Ramu Murakami Gutierrez, Gerente de Produtos, agosto de 2023