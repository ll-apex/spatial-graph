# Usar Análise de Gráficos para Recomendar Filmes

## Introdução

Neste workshop, você usará o Graph Studio para detectar e criar comunidades de clientes com base no comportamento de visualização de filmes. Depois de criar comunidades - faça recomendações com base no que os membros da comunidade observaram.

Tempo Estimado: 60 minutos

### Sobre o Graph Studio

O Oracle Autonomous Database tem recursos que permitem que ele funcione como um banco de dados gráfico de propriedades escalável. Eles automatizam a criação de modelos gráficos e gráficos na memória com base em tabelas de banco de dados. Eles incluem notebooks e APIs do desenvolvedor para executar consultas gráficas usando PGQL, uma linguagem de consulta gráfica semelhante a SQL e mais de 60 algoritmos gráficos incorporados e muitas visualizações, incluindo visualização gráfica nativa.

Assista ao vídeo a seguir que apresenta uma introdução aos gráficos de propriedades e seus casos de uso.

Simplificar Análises Gráficos com o Autonomous Database

[](youtube:eCd-969hrak)

Neste workshop, você usará um gráfico criado com base nas tabelas MOVIE, CUSTOMER\_PROMOTIONS e CUSTSALES\_PROMOTIONS. MOVIE e CUSTOMER\_PROMOTIONS são tabelas de vértices (cada linha nessas tabelas se torna um vértice). CUSTSALES\_PROMOTIONS conecta as duas tabelas e é a tabela de borda. Toda vez que um cliente em CUSTOMER\_PROMOTIONS aluga um filme na tabela FILME, isso é uma borda no gráfico. Este gráfico foi criado para você usar neste workshop.

Você tem a opção de mais de 60 algoritmos pré-criados ao analisar um gráfico. Neste workshop, você usará o algoritmo **SALSA Personalizado**, que é uma boa opção para recomendações de produtos. Os vértices do cliente são mapeados para _hubs_ e os filmes são mapeados para _autoridades_. Pontuações mais altas de hub indicam um relacionamento mais próximo entre os clientes. Pontuações mais altas de autoridade indicam que o vértice (ou filme) desempenha um papel mais importante no estabelecimento dessa proximidade.

### Objetivos

Neste workshop, você usará o recurso Graph Studio do Autonomous Database para:

*   Usar um notebook
*   Executar algumas consultas de gráfico PGQL
*   Usar python para executar o SALSA Personalizado na biblioteca de algoritmos
*   Pesquisar e salvar as recomendações

### Pré-requisitos

*   Conta do Oracle Cloud

## Agradecimentos

*   **Autor** - Melli Annamalai, Gerente de Produtos, Oracle Spatial and Graph
*   **Colaboradores** - Jayant Sharma
*   **Última Atualização em/Data** - Ramu Murakami Gutierrez, Gerente de Produtos, Oracle Spatial and Graph, fevereiro de 2023