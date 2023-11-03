# 创建样本数据

## 简介

此实验室将指导您完成在 Oracle Database 中创建示例空间数据的步骤。

估计的实验室时间：10 分钟

### 目标

在此实验室中，您将：

*   了解 Oracle Database 中的空间数据管理
*   使用常用文件格式准备 Oracle Database 中的空间数据

### 先备条件

*   完成实验室 2

### 关于空间数据

Oracle Database 将空间数据（点、线、多边形）存储在名为 SDO\_GEOMETRY 的本机数据类型中。Oracle Database 还提供了用于高性能空间操作的原生空间索引。此空间索引依赖于为每个表输入的空间元数据以及存储空间数据的几何列。填充空间数据并为其编制索引后，可以使用强大的 API 执行空间分析、计算和处理。

SDO\_GEOMETRY 类型具有以下常规格式：

    SDO_GEOMETRY( 
     [geometry type],           --ID for point/line/polygon
     [coordinate system],       --ID of coordinate system
     [point coordinate],        --for points only
     [line/polygon info],       --for lines/polygons only
     [line/polygon coordinates] --for lines/polygons only
      )
    

最常见的几何类型是 2 维：

| ID | 类型 |
| --- | --- |
| 2001 年 | 点数 |
| 2002 年 | 行 |
| 2003 | 多边形 |

最常见的坐标系有：

| ID | 坐标系 |
| --- | --- |
| 4326 | 纬度/长度 |
| 3857 | World Mercator |

使用纬度/经度时，请注意，纬度是 Y 坐标，经度是 X 坐标。由于坐标列为 X、Y 对，因此值实际上按经度和纬度顺序排列。

以下是使用纬度/经度坐标的点几何图形示例：

    SDO_GEOMETRY( 
     2001,               --2D point
     4326,               --latitude/longitude
     SDO_POINT_TYPE(     
        -100.123, 20.456 --coordinate
        ),         
     NULL,               --for lines/polygons only
     NULL                --for lines/polygons only
      )
    

以下是使用纬度/经度坐标的多边形几何图形示例：

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
    

### 目标

在此实验室中，您将：

*   使用几何列创建表
*   填充几何图形
*   创建空间元数据和索引

### 先备条件

如研习会简介中所述，您需要访问 Oracle Database 和 SQL Client。如果您没有这些功能，请返回到 Oracle Cloud 账户、Autonomous Database 和 SQL Developer Web 上的各个部分。

## 任务 1：创建具有坐标的表

首先创建具有纬度、经度坐标的表。这是创建空间数据的常见起点，例如来自 GPS 的坐标，或来自地理编码街道地址或 IP 地址。

指令和屏幕截图引用 SQL Developer Web，但适用于其他 SQL 客户端的步骤相同。

1.  在[此处](files/create-sample-data.sql)下载 SQL 脚本。
    
2.  在 SQL Developer Web 中复制/粘贴/运行脚本 ![图像替代文本](images/run-script-1.png)
    
3.  刷新列表以查看表 BRANCHES 和 WAREHOUSES
    
    ![图像替代文本](images/refresh-tables-1.png)
    

## 任务 2：根据坐标创建几何图形

对于 exathis 情况，可以通过基于纬度和经度列指定点几何的坐标来填充几何。

1.  添加几何列：
    
        <copy> 
        ALTER TABLE WAREHOUSES ADD (
         GEOMETRY SDO_GEOMETRY
        );
        
        ALTER TABLE BRANCHES ADD (
           GEOMETRY SDO_GEOMETRY
        );
        </copy>
        
2.  填充几何列：
    
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
        

## 任务 3：使用多边形创建表

可以以相同的方式创建行和多边形。虽然点几何体需要一个坐标，但线和多边形需要定义几何体的所有坐标。在本例中，我们创建一个表来存储多边形。

1.  创建表并插入行
    
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
        
2.  刷新表列表以查看 COASTAL\_ZONE 表。 ![图像替代文本](images/refresh-tables-2.png)
    

## 任务 4：添加空间元数据和索引

Oracle Database 为高性能空间操作提供了一个原生空间索引。我们的样本数据非常小，因此不需要空间索引。但是，我们执行以下步骤，因为它们对典型的生产数据量非常重要。空间索引要求为要编制索引的几何对象提供一行元数据。我们先创建此元数据，然后创建空间索引。

1.  添加空间元数据：
    
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
        
2.  创建空间索引：
    
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
        
    
    创建索引后，刷新表列表。您将看到 3 个表的名称以 MDRT\_ 开头。这些是空间索引的对象，由 Oracle Database 自动管理。切勿手动处理这些表。 ![图像替代文本](images/refresh-tables-3.png)
    
    我们的样本数据现已准备就绪，可用于空间查询。
    
    现在，您可以进入下一个实验室。
    
    如果需要恢复此实验室并删除创建的项，请运行以下命令：
    
         DROP TABLE BRANCHES;   
         DROP TABLE WAREHOUSES;
         DROP TABLE COASTAL_ZONE;
         DELETE FROM USER_SDO_GEOM_METADATA;
         COMMIT;
        

## 了解详细信息

*   ［空间产品门户］ (https://oracle.com/goto/spatial)
*   [空间文档](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [空间博客](https://blogs.oracle.com/oraclespatial/)

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - Kamryn Vinson，2020 年 11 月