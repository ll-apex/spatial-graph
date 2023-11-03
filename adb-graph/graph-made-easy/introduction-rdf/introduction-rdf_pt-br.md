# Trabalhar com Gráficos RDF no Graph Studio

## Introdução

O Graph Studio no Oracle Autonomous Database permite que os usuários modelem, criem, consultem e analisem dados gráficos. Ele inclui notebooks, APIs do desenvolvedor para executar consultas gráficas usando PGQL, mais de 60 algoritmos gráficos incorporados e oferece dezenas de visualizações, incluindo visualização gráfica nativa. Além do gráfico de propriedades, o Graph Studio agora estende o suporte a tecnologias semânticas, incluindo recursos de armazenamento, inferência e consulta para dados e ontologias com base no Resource Description Framework (RDF) e na Web Ontology Language (OWL). Agora você pode usar o Graph Studio para os seguintes recursos RDF suportados:

*   Criar um gráfico RDF
*   Executar consultas SPARQL no gráfico RDF em um parágrafo de notebook
*   Analisar e visualizar gráficos RDF

O RDF é um modelo de dados padrão W3C para representar dados vinculados. O RDF usa URIs (Uniform Resource Identifiers) como identificadores globalmente exclusivos para recursos e URIs para nomear o relacionamento entre dois recursos. Além dos URIs, o RDF usa literais para representar valores escalares, como números, strings e timestamps. O RDF modela dados vinculados como um gráfico direcionado e rotulado, onde cada borda é geralmente chamada de tripla. O vértice de origem da borda é chamado de sujeito do triplo. O rótulo ou nome da borda é chamado de predicado do triplo, e o vértice de destino da borda é chamado de objeto do triplo. Os gráficos RDF são particularmente adequados para gráficos de conhecimento e aplicativos de integração de dados porque os URIs fornecem identificadores globalmente exclusivos e a estrutura tripla simples e sem esquema facilita muito a combinação de dados de vários gráficos RDF diferentes em um único gráfico. Além disso, o RDFS e o OWL fornecem maneiras padrão de definir vocabulários reutilizáveis (conjuntos de rótulos de borda semanticamente significativos e tipos de recursos) para dados gráficos mais interoperáveis e processáveis por máquina. Veja [aqui](https://www.w3.org/TR/rdf11-primer/) mais informações sobre os padrões W3C RDF 1.1.

O SPARQL Protocol and RDF Query Language (SPARQL) é uma das tecnologias padronizadas pelo W3C para consultar dados do Resource Description Framework (RDF). Você pode ler mais sobre o padrão SPARQL 1.1 W3C [aqui](https://www.w3.org/TR/sparql11-overview/).

SPARQL usa uma estrutura **SELECT alguns elementos WHERE algumas condições** para especificar uma consulta. As condições na cláusula WHERE de uma consulta SPARQL são criadas usando padrões triplos, que são essencialmente um triplo RDF, onde os elementos do triplo podem ser substituídos por variáveis de consulta (indicados com um prefixo ?). Uma variável de consulta em um padrão triplo atua como um curinga. Considere o padrão triplo **?movie ms:genre ms:genre\_Comedy**. Quando esse padrão triplo for avaliado em um gráfico RDF, ele retornará todos os **sujeitos** de triplos com predicado **ms:genre** e **objeto ms:genre\_Comedy**. A cláusula SPARQL SELECT especifica uma lista de variáveis de consulta a serem projetadas com base na consulta. Na sintaxe SPARQL, os URIs estão entre colchetes angulares (por exemplo, [http://www.example.com/moviestream/actor](http://www.example.com/moviestream/actor)) e os literais estão entre aspas duplas (por exemplo, "Kevin Bacon"). Os literais podem ser seguidos por ^^ e um URI de tipo de dados (por exemplo, "100"^^[http://www.w3.org/2001/XMLSchema#integer](http://www.w3.org/2001/XMLSchema#integer)) ou seguidos por @ e uma tag de idioma (por exemplo, "Jalapeño"@es). A maioria dos tipos de dados do esquema XML são suportados em SPARQL, e literais simples sem um URI de tipo de dados são considerados como tendo o tipo de dados [http://www.w3.org/2001/XMLSchema#string](http://www.w3.org/2001/XMLSchema#string).

Este vídeo apresentado abaixo é um exemplo de demonstração usando um conjunto de dados semelhante que será utilizado neste laboratório. Este vídeo enfatiza a estrutura da ontologia da estrutura do filme usando RDF. A demonstração apresenta o RDF Graph usando uma tabela intermediária em combinação com o SQL Developer, que é distintamente diferente dessa versão do laboratório do Autonomous Database. No entanto, a linguagem SPARQL usada para consultar e visualizar os dados é muito semelhante para o contexto.

[Exemplo de demonstração do uso do RDF](youtube:e_EQjInas50)

Neste laboratório, um gráfico semântico será construído usando SPARQL, que é uma metodologia padronizada para integrar diferentes fontes de dados. Este procedimento ensinará como analisar os dados usando consultas e visualização baseadas em gráficos.

Tempo Estimado: 25 minutos

### Objetivos

*   Conceitos Básicos de Gráficos RDF
*   Consultando e Visualizando o Gráfico RDF

### Pré-requisitos

*   O laboratório a seguir requer uma conta do Autonomous Database - Shared Infrastructure.
*   E que o usuário habilitado para Gráfico (GRAPHUSER) existe. Ou seja, existe um usuário de banco de dados com as atribuições e os privilégios corretos.

Isso conclui este laboratório. Agora você pode **prosseguir para o próximo laboratório.**

## Agradecimentos

*   **Autor** - Nicholas Cusato, Ethan Shmargad, Matthew McDaniel Engenheiros de Soluções, Gerente de Produtos Ramu Murakami Gutierrez
*   **Contribuinte Técnico** - Melliyal Annamalai Gerente de Produto, Joao Paiva Consulting Membro da Equipe Técnica, Lavanya Jayapalan Principal User Assistance Developer
*   **Última Atualização em/Data** - Ramu Murakami Gutierrez, Gerente de Programa, junho de 2022