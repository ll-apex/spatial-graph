# Explorar Dados

## Introdução

Agora você explora os dados de locais e transações preparados no laboratório anterior. Ao gerenciar os dados no Autonomous Database, você pode executar operações de processamento e análise de back-end e, em seguida, trazer subconjuntos de dados apropriados para o Python para análises especializadas.

Tempo de Laboratório Estimado: 10 minutos

### Objetivos

*   Traga dados espaço-temporais e resultados de consulta do Autonomous Database para o Python
*   Visualizar e explorar os dados em Python

### Pré-requisitos

*   Conclusão do Laboratório 5: Preparar dados

## Tarefa 1: Tratamento de dados espaciais no Python

A biblioteca Python mais comum para tratamento de dados é o Pandas, que fornece DataFrame como a estrutura de dados semelhante a uma tabela com colunas e linhas. A biblioteca GeoPandas estende o Pandas para tratamento de dados espaciais, em que DataFrame é estendido para GeoDataFrame, incluindo uma coluna "geometria". A biblioteca Shapely fornece o tipo espacial usado para preencher a coluna de geometria. O Folium é uma biblioteca popular de visualização de mapas e é usado por GeoPandas.

1.  Importe bibliotecas para tratamento de dados espaciais e visualização de mapas.
    
        <copy>
        import geopandas as gpd
        import shapely
        import folium
        </copy>
        
    
    ![Explorar dados](images/explore-data-01.png)
    
2.  Como exemplo básico de dados espaciais em Python, execute o seguinte para criar manualmente um GeoDataFrame contendo locais de pontos para várias cidades. Os valores de geometria estão no formato Texto Bem Conhecido ("WKT"), pois esse é o formato usado em um GeoDataFrame.
    
        <copy>
        gdf = gpd.GeoDataFrame(
          {
            "city": ["Buenos Aires", "Brasilia", "Santiago", "Bogota", "Caracas"],
            "country": ["Argentina", "Brazil", "Chile", "Colombia", "Venezuela"],
            "geometry": ["POINT(-58.66 -34.58)",
                         "POINT(-47.91 -15.78)",
                         "POINT(-70.66 -33.45)",
                         "POINT(-74.08 4.60)",
                         "POINT(-66.86 10.48)",
                ],})
        gdf["geometry"] = gpd.GeoSeries.from_wkt(gdf["geometry"])
        gdf.set_geometry("geometry")
        gdf.crs="EPSG:4326"
        gdf
        </copy>
        
    
    ![Explorar dados](images/explore-data-02.png)
    
3.  Para visualizar os dados, execute o seguinte, onde você especifica o mapa de plano de fundo e o tamanho do marcador. Mova o mouse sobre um marcador de mapa para ver seus atributos.
    
        <copy>
        gdf.explore(tiles="CartoDB positron", marker_kwds={"radius":8})
        </copy>
        
    
    ![Explorar dados](images/explore-data-03.png)
    
4.  O Oracle Spatial inclui funções e métodos para conversão do tipo espacial nativo em formatos comuns, incluindo conversão para o formato WKT usado em um GeoDataFrame. Portanto, a criação de um GeoDataFrame com base nos resultados do Oracle Spatial é simples. A sintaxe de conversão de métodos de objetos é mais compacta que as funções SQL equivalentes. Por exemplo, o método **(geometry).get\_wkt()** versus a função **sdo\_util.to\_wktgeometry(geometry)**. Execute o seguinte para ver um exemplo básico de conversões de formato de um SDO\_GEOMETRY hard-coded para formatos WKT e GeoJSON usando métodos de objeto.
    

    ```
    <copy>
    cursor = connection.cursor()
    cursor.execute("""
      WITH x AS (
        SELECT sdo_geometry(2001,4326,sdo_point_type(-100.12, 22.34,null),null,null) 
               as geometry
        FROM dual)
      SELECT geometry, 
             (geometry).get_wkt(), 
             (geometry).get_geojson()
      FROM x
      """)
    for row in cursor.fetchone():
       print(row)
    </copy>
    ```
    ![Explore data](images/explore-data-04.png) 
    

5.  No laboratório anterior, você configurou a tabela LOCATIONS com um índice espacial baseado em função. A função é lonlat\_to\_proj\_geom( ) e converte longitude, latitude em SDO\_GEOMETRY no sistema de coordenadas World Mercator para compatibilidade com bibliotecas usadas em um laboratório posterior. Execute o seguinte para recuperar geometrias usando essa função como formato WKT.

    ```
    <copy>
    cursor = connection.cursor()
    cursor.execute("""
      SELECT lon, lat, (lonlat_to_proj_geom(lon,lat)).get_wkt()
      FROM locations
      """)
    for row in cursor.fetchmany(10):
       print(row)
    </copy>
    ```
    ![Explore data](images/explore-data-05.png) 
    

6.  Execute o seguinte para recuperar a tabela LOCATIONS e criar um GeoDataFrame.
    
        <copy>
        cursor.execute("""
         SELECT location_id, owner, (lonlat_to_proj_geom(lon,lat)).get_wkt()
         FROM locations
         """)
        gdf = gpd.GeoDataFrame(cursor.fetchall(), columns = ['location_id', 'owner', 'geometry'])
        gdf['geometry'] = shapely.from_wkt(gdf['geometry'])
        gdf.crs="EPSG:3857"
        gdf.head()
        </copy>
        
    
    ![Explorar dados](images/explore-data-06.png)
    
7.  Execute o seguinte para visualizar o GeoDataFrame.
    
        <copy>
        gdf.explore(tiles="CartoDB positron")
        </copy>
        
    
    ![Explorar dados](images/explore-data-07.png)
    

## Tarefa 2: Explorar dados de transações

1.  Em seguida, você cria um GeoDataFrame de uma consulta que une TRANSACTIONS a LOCATIONS. Execute o seguinte para criar o GeoDataFrame.
    
        <copy>
        cursor = connection.cursor()
        cursor.execute("""
         SELECT a.cust_id, a.trans_id, a.trans_epoch_date, 
          (lonlat_to_proj_geom(b.lon,b.lat)).get_wkt() 
         FROM transactions a, locations b
         WHERE a.location_id=b.location_id
         """)
        gdf = gpd.GeoDataFrame(cursor.fetchall(), columns = ['cust_id', 'trans_id', 'trans_epoch_date', 'geometry'])
        gdf['geometry'] = shapely.from_wkt(gdf['geometry'])
        gdf.crs="EPSG:3857"
        gdf.head()
        </copy>
        
    
    ![Explorar dados](images/explore-data-08.png)
    
2.  Execute o seguinte para visualizar o GeoDataFrame. Passe o mouse sobre um item para ver os atributos da transação.
    
        <copy>
        gdf.explore(tiles="CartoDB positron") 
        </copy>
        
    
    ![Explorar dados](images/explore-data-09.png)
    

Agora você pode **prosseguir para o próximo laboratório**.

## Saiba Mais

*   Para obter detalhes sobre GeoPandas, consulte [https://geopandas.org](https://geopandas.org)

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Colaboradores** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Última Atualização em/Data** - David Lapp, agosto de 2023