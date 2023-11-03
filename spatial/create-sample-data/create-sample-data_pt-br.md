# Criar dados de amostra

## Introdução

Este laboratório apresenta as etapas para criar dados espaciais de amostra no Oracle Database.

Tempo de Laboratório Estimado: 10 minutos

### Objetivos

Neste laboratório, você vai:

*   Saiba mais sobre o gerenciamento de dados espaciais no Oracle Database
*   Preparar dados espaciais no Oracle Database a partir de formatos de arquivo comuns

### Pré-requisitos

*   Conclusão do Laboratório 2

### Sobre dados espaciais

O Oracle Database armazena dados espaciais (pontos, linhas, polígonos) em um tipo de dados nativo chamado SDO\_GEOMETRY. O Oracle Database também fornece um índice espacial nativo para operações espaciais de alto desempenho. Esse índice espacial depende de metadados espaciais que são inseridos para cada tabela e coluna de geometria que armazena dados espaciais. Uma vez que os dados espaciais são preenchidos e indexados, APIs robustas estão disponíveis para realizar análise espacial, cálculos e processamento.

O tipo SDO\_GEOMETRY tem o seguinte formato geral:

    SDO_GEOMETRY( 
     [geometry type],           --ID for point/line/polygon
     [coordinate system],       --ID of coordinate system
     [point coordinate],        --for points only
     [line/polygon info],       --for lines/polygons only
     [line/polygon coordinates] --for lines/polygons only
      )
    

Os tipos de geometria mais comuns são 2-dimensional:

| ID | Tipo |
| --- | --- |
| 2001 | Ponto |
| 2002 | Linha |
| 2003 | Polygon |

Os sistemas de coordenadas mais comuns são:

| ID | Sistema Coordenado |
| --- | --- |
| 4326 | Latitude/Longitude |
| 3857 | Mercator Mundial |

Ao usar latitude/longitude, observe que a latitude é a coordenada Y e a longitude é a coordenada X. Como as coordenadas são listadas como par X, Y, os valores estão, na verdade, na ordem de longitude, latitude.

Veja a seguir um exemplo de geometria de ponto usando coordenadas de latitude/longitude:

    SDO_GEOMETRY( 
     2001,               --2D point
     4326,               --latitude/longitude
     SDO_POINT_TYPE(     
        -100.123, 20.456 --coordinate
        ),         
     NULL,               --for lines/polygons only
     NULL                --for lines/polygons only
      )
    

Veja a seguir um exemplo de geometria de polígono usando coordenadas de latitude/longitude:

    SDO_GEOMETRY( 
     2003,                  --2D polygon
     4326,                  --latitude/longitude
     NULL,                  --for points only       
     SDO_ELEM_INFO_ARRAY(
          1, 1003, 1        --indicates simple exterior polygon
            ), 
     SDO_ORDINATE_ARRAY(   
        -98.789065,39.90973, -- coordinates
        -101.2522,39.639537,
        -99.84374,37.160316,
        -96.67987,35.460699,
        -94.21875,39.639537,
        -98.789025,39.90973
          )
        )
    );
    

### Objetivos

Neste laboratório, você vai:

*   Criar tabelas com uma coluna de geometria
*   Preencher geometrias
*   Criar metadados e índices espaciais

### Pré-requisitos

Conforme descrito na introdução do workshop, você precisa de acesso a um Oracle Database e SQL Client. Se você não tiver essas opções, volte às seções da Oracle Cloud Account, Autonomous Database e SQL Developer Web.

## Tarefa 1: Criar tabelas com coordenadas

Começamos criando tabelas com coordenadas de latitude e longitude. Este é um ponto de partida comum para criar dados espaciais, por exemplo, coordenadas de GPS, ou de geocodificação de endereço de rua ou endereço IP.

As instruções e as capturas de tela se referem ao SQL Developer Web. No entanto, as mesmas etapas se aplicam a outros clientes SQL.

1.  Faça download do script SQL [aqui](files/create-sample-data.sql).
    
2.  Copiar/colar/executar o script no SQL Developer Web ![Texto alternativo da imagem](images/run-script-1.png)
    
3.  Atualize a listagem para ver as tabelas BRANCHES e WAREHOUSES
    
    ![Texto alternativo da imagem](images/refresh-tables-1.png)
    

## Tarefa 2: Criar geometrias a partir de coordenadas

As geometrias podem ser preenchidas com SQL, para exathis case, especificando as coordenadas das geometrias de ponto com base nas colunas de latitude e longitude.

1.  Adicionar colunas de geometria:
    
        <copy> 
        ALTER TABLE WAREHOUSES ADD (
         GEOMETRY SDO_GEOMETRY
        );
        
        ALTER TABLE BRANCHES ADD (
           GEOMETRY SDO_GEOMETRY
        );
        </copy>
        
2.  Preencher colunas de geometria:
    
        <copy> 
        UPDATE WAREHOUSES
        SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
         UPDATE BRANCHES
         SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
        </copy>
        

## Tarefa 3: Criar tabela com polígono

Linhas e polígonos podem ser criados da mesma maneira. Enquanto uma geometria de ponto requer uma coordenada, linhas e polígonos requerem todas as coordenadas que definem a geometria. Nesse caso, criamos uma tabela para armazenar um polígono.

1.  Criar tabela e inserir linha
    
        <copy>
        CREATE TABLE COASTAL_ZONE (
            ZONE_ID   NUMBER,
            GEOMETRY  SDO_GEOMETRY
        );       
        
        INSERT INTO COASTAL_ZONE VALUES (
            1,
            SDO_GEOMETRY(
                2003, 4326, NULL, SDO_ELEM_INFO_ARRAY(
                    1, 1003, 1
                ), SDO_ORDINATE_ARRAY(
                    -93.719934, 30.210638,
                    -95.422592, 29.773714, 
                    -95.059698, 29.322204, 
                    -96.013892, 28.787021, 
                    -96.660964, 28.925638, 
                    -97.528688, 28.042050, 
                    -97.858501, 27.447461, 
                    -97.497364, 25.880056, 
                    -96.977826, 25.969716, 
                    -97.211445, 27.054605, 
                    -96.870226, 27.816077, 
                    -93.794290, 29.535729, 
                    -93.719934, 30.210638
                )
            )
        );
        </copy>
        
2.  Atualize a listagem de tabelas para ver a tabela COASTAL\_ZONE. ![Texto alternativo da imagem](images/refresh-tables-2.png)
    

## Tarefa 4: Adicionar metadados e índices espaciais

O Oracle Database fornece um índice espacial nativo para operações espaciais de alto desempenho. Nossos dados de amostra são tão pequenos que um índice espacial não é realmente necessário. No entanto, realizamos as etapas a seguir, pois elas são importantes para volumes de dados de produção típicos. Um índice espacial requer uma linha de metadados para a geometria que está sendo indexada. Criamos esses metadados e, em seguida, os índices espaciais.

1.  Adicione metadados espaciais:
    
        <copy> 
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'WAREHOUSES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'BRANCHES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'COASTAL_ZONE',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        </copy>
        
2.  Criar índices espaciais:
    
        <copy> 
        CREATE INDEX WAREHOUSES_SIDX ON
            WAREHOUSES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX BRANCHES_SIDX ON
            BRANCHES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX COASTAL_ZONE_SIDX ON
            COASTAL_ZONE (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
         </copy>
        
    
    Depois que os índices forem criados, atualize a listagem de tabelas. Você verá 3 tabelas com nomes que começam com MDRT\_. Esses são artefatos dos índices espaciais e são gerenciados pelo Oracle Database automaticamente. Essas tabelas nunca devem ser manipuladas manualmente. ![Texto alternativo da imagem](images/refresh-tables-3.png)
    
    Nossos dados de amostra agora estão preparados e prontos para consultas espaciais.
    
    Agora você pode ir para o próximo laboratório.
    
    Se você precisar reverter este laboratório e remover os itens criados, execute o seguinte:
    
         DROP TABLE BRANCHES;   
         DROP TABLE WAREHOUSES;
         DROP TABLE COASTAL_ZONE;
         DELETE FROM USER_SDO_GEOM_METADATA;
         COMMIT;
        

## Saiba mais

*   \[Portal de produtos espaciais\] (https://oracle.com/goto/spatial)
*   [Documentação espacial](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Blogs espaciais](https://blogs.oracle.com/oraclespatial/)

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - Kamryn Vinson, novembro de 2020