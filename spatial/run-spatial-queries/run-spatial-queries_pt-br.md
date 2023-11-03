# Consultas Espaciais

## Introdução

Este laboratório orienta você nas consultas espaciais básicas no Oracle Database. Você usará os dados de amostra criados no laboratório anterior para identificar itens com base na proximidade e na contenção.

Tempo de Laboratório Estimado: 15 minutos

### Sobre Consultas Espaciais

O Oracle Database inclui uma biblioteca robusta de funções e operadores para análise espacial. Isso inclui relações espaciais, medições, agregações, transformações e muito mais. Essas operações podem ser acessadas por meio de SQL nativo, PL/SQL, APIs Java e qualquer outra linguagem que se comunique com o Oracle Database.

### Objetivos

Neste laboratório, você vai:

*   Identificar BRANCHES que têm relacionamentos de proximidade com um DEPÓSITO
*   Identificar BRANCAS que têm relacionamentos de contenção e proximidade com um COASTAL\_ZONE

### Pré-requisitos

*   Conclusão do laboratório anterior; Criar Dados Espaciais de Amostra

## Consultas Espaciais

As consultas espaciais no Oracle Database são como qualquer outra consulta tradicional à qual você está acostumado. A única diferença é um conjunto de funções espaciais e operadores que provavelmente são novos para você.

**Identifique as 5 filiais mais próximas do Dallas Warehouse:**

    <copy> 
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5'
        ) = 'TRUE';
    </copy>
    

![Executar consulta espacial](images/query1.png) Observações:

*   O operador `SDO_NN` retorna as ramificações 'n mais próximas' para o Dallas Warehouse, em que 'n' é o valor especificado para `SDO_NUM_RES`. O primeiro argumento para `SDO_NN` (`B.GEOMETRY` no exemplo acima) é a coluna a ser pesquisada. O segundo argumento (`W.GEOMETRY` no exemplo acima) é o local ao qual você deseja encontrar os vizinhos mais próximos. Nenhuma suposição deve ser feita sobre a ordem dos resultados retornados. Por exemplo, não é garantido que a primeira linha retornada seja a mais próxima. Se duas ou mais ramificações estiverem a uma distância igual do warehouse, elas poderão ser retornadas em chamadas subsequentes para `SDO_NN`.
*   Ao usar o parâmetro `SDO_NUM_RES`, nenhum outro critério é usado na cláusula `WHERE`. `SDO_NUM_RES` leva apenas em consideração a proximidade. Por exemplo, se você adicionasse um critério à cláusula `WHERE` porque queria que as cinco ramificações mais próximas tivessem um CEP específico e quatro das cinco ramificações mais próximas tivessem um CEP diferente, a consulta acima retornaria uma linha. Esse comportamento é específico do parâmetro `SDO_NUM_RES`. Em uma consulta abaixo, você usará um parâmetro alternativo para o cenário de critérios de consulta adicionais.

**Identifique as 5 filiais mais próximas do Dallas Warehouse com distância:**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5 unit=km', 1
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Executar consulta espacial](images/query2.png) Observações:

*   O operador `SDO_NN_DISTANCE` é um operador auxiliar do operador `SDO_NN`; ele só pode ser usado dentro do operador `SDO_NN`. O argumento para este operador é um número que corresponde ao número especificado como o último argumento de `SDO_NN`; neste exemplo, é 1. Não há significado oculto para este argumento, é simplesmente uma tag. Se `SDO_NN_DISTANCE()` for especificado, você poderá ordenar os resultados por distância e garantir que a primeira linha retornada seja a mais próxima. Se os dados que você está consultando forem armazenados como longitude e latitude, a unidade padrão para `SDO_NN_DISTANCE` será metros.
*   O operador `SDO_NN` também tem um parâmetro `UNIT` que determina a unidade de medida retornada por `SDO_NN_DISTANCE`.
*   A cláusula `ORDER BY DISTANCE` garante que as distâncias sejam retornadas em ordem, com a distância mais curta primeiro.

**Identifique as 5 ramificações WHOLESALE mais próximas do Dallas Warehouse com a distância:**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND B.BRANCH_TYPE = 'WHOLESALE'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_batch_size=5 unit=km', 1
        ) = 'TRUE'
        AND ROWNUM <= 5
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Executar consulta espacial](images/query3.png) Observações:

*   `SDO_BATCH_SIZE` é um parâmetro ajustável que pode afetar o desempenho da consulta. `SDO_NN` calcula internamente esse número de distâncias por vez. O batch inicial de linhas retornadas pode não atender às constraints na cláusula WHERE. Portanto, o número de linhas especificadas por `SDO_BATCH_SIZE` é continuamente retornado até que todas as constraints na cláusula WHERE sejam satisfeitas. Escolha um `SDO_BATCH_SIZE` que retorne inicialmente o número de linhas que provavelmente satisfaçam as constraints na cláusula WHERE.
*   O parâmetro `UNIT` usado no operador `SDO_NN` especifica a unidade de medida do parâmetro `SDO_NN_DISTANCE`. A unidade padrão é a unidade de medida associada aos dados. Para dados de longitude e latitude, o padrão é metros.
*   `B.BRANCH_TYPE = 'WHOLESALE' AND ROWNUM <= 5` são as restrições adicionais na cláusula `WHERE`. A cláusula rownum é necessária para limitar o número de resultados retornados a 5.
*   A cláusula `ORDER BY DISTANCE_KM` garante que as distâncias sejam retornadas em ordem, com a distância mais curta primeiro e as distâncias medidas em milhas.

**Identifique filiais dentro de 50km de Houston Warehouse:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE';
    </copy>
    

![Executar consulta espacial](images/query4.png) Observações:

*   O primeiro argumento para `SDO_WITHIN_DISTANCE` é a coluna a ser pesquisada. O segundo argumento é o local a partir do qual você deseja determinar as distâncias. Nenhuma suposição deve ser feita sobre a ordem dos resultados retornados. Por exemplo, não é garantido que a primeira linha retornada seja o cliente mais próximo do depósito 3.
*   O parâmetro DISTANCE usado dentro do operador `SDO_WITHIN_DISTANCE` especifica o valor da distância; neste exemplo, é 100.
*   O parâmetro UNIT usado no operador `SDO_WITHIN_DISTANCE` especifica a unidade de medida do parâmetro DISTANCE. A unidade padrão é a unidade de medida associada aos dados. Para dados de longitude e latitude, o padrão é metros; neste exemplo, são milhas.

**Identifique filiais dentro de 50 km de Houston Warehouse com distância:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE,
        ROUND(
            SDO_GEOM.SDO_DISTANCE(
                B.GEOMETRY, W.GEOMETRY, 0.05, 'unit=km'
            ), 2
        ) AS DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![Executar consulta espacial](images/query5.png) Observações:

*   A função `SDO_GEOM.SDO_DISTANCE` calcula a distância entre as filiais e o Houston Warehouse.
*   Os primeiros 2 argumentos para `SDO_GEOM.SDO_DISTANCE` são locais BRANCH e WAREHOUSE para cálculo de distância.
*   O terceiro argumento para `SDO_GEOM.SDO_DISTANCE` é o valor de tolerância. A tolerância é um valor de erro de arredondamento usado pelo Oracle Spatial. A tolerância está em metros para dados de longitude e latitude. Neste exemplo, a tolerância é de 50 mm.
*   O parâmetro UNIT usado no parâmetro `SDO_GEOM.SDO_DISTANCE` especifica a unidade de medida da distância calculada pela função `SDO_GEOM`.`SDO_DISTANCE`. A unidade padrão é a unidade de medida associada aos dados. Para dados de longitude e latitude, o padrão é metros. Neste exemplo são milhas.
*   A cláusula `ORDER BY DISTANCE_IN_MILES` garante que as distâncias sejam retornadas em ordem, com a distância mais curta primeiro e as distâncias medidas em milhas.

**Identificar ramos na zona costeira:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE';
    </copy>
    

![Executar consulta espacial](images/query6.png) Observações:

*   O operador `SDO_ANYINTERACT` aceita 2 argumentos, geometry1 e geometry2. O operador retorna `TRUE` para linhas em que geometry1 está dentro ou no limite de geometry2.
*   Neste exemplo, geometry1 é `B.GEOMETRY`, as geometrias da ramificação e geometry2 é `C.GEOMETRY`, a geometria da zona costeira. A tabela COASTAL\_ZONE tem apenas 1 linha; portanto, nenhum critério adicional é necessário.

**Identificar ramos fora e dentro de 10 km da zona costeira:**

    <copy>
    
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_WITHIN_DISTANCE(
            B.GEOMETRY, C.GEOMETRY, 'distance=10 unit=km'
        ) = 'TRUE'
    )
    MINUS
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE'
    );
    </copy>
    

![Executar consulta espacial](images/query7.png) Observações:

*   Na primeira parte dessa consulta, o operador `SDO_WITHIN_DISTANCE` identifica BRANQUES a 10 km do COASTAL\_ZONE. Isso inclui BRANCHES dentro do COASTAL\_ZONE.
*   A consulta usa `MINUS` para remover BRANCHES dentro do COASTAL\_ZONE, deixando apenas BRACNCHES dentro de 10 km e fora do COASTAL\_ZONE.

## Saiba Mais

*   \[Portal de produtos espaciais\] (https://oracle.com/goto/spatial)
*   [Documentação espacial](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Blogs espaciais](https://blogs.oracle.com/oraclespatial/)

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - Kamryn Vinson, novembro de 2020