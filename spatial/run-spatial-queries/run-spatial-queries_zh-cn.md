# 空间查询

## 简介

此实验室将指导您完成 Oracle Database 中的基本空间查询。您将使用在上一个实验室中创建的示例数据基于邻近性和包含性来标识项。

估计的实验室时间：15 分钟

### 关于空间查询

Oracle Database 包含强大的函数和运算符库，可用于空间分析。这包括空间关系、测量、聚合、转换等。可以通过本机 SQL、PL/SQL、Java API 以及任何其他与 Oracle Database 通信的语言访问这些操作。

### 目标

在此实验室中，您将：

*   标识与仓库具有邻近关系的分行
*   标识与 COASTAL\_ZONE 具有包含和接近关系的分支

### 先备条件

*   完成上一个实验室；创建样本空间数据

## 空间查询

Oracle Database 中的空间查询与您习惯的任何其他传统查询一样。唯一的区别是一组空间函数和运算符，这些函数和运算符对您来说可能是新的。

**确定距离达拉斯仓库最近的 5 个分支：**

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
    

![运行空间查询](images/query1.png) 备注：

*   `SDO_NN` 运算符返回到 Dallas Warehouse 的 'n nearest' 分支，其中 'n' 是专用于 `SDO_NUM_RES` 的值。`SDO_NN` 的第一个参数（在上例中为 `B.GEOMETRY`）是要搜索的列。第二个参数（在上面的示例中为 `W.GEOMETRY`）是您希望找到最接近的邻居的位置。不应该对返回结果的顺序做出任何假设。例如，返回的第一行不能保证是最接近的行。如果两个或多个分支与仓库的距离相等，则可在后续调用 `SDO_NN` 时返回任一分支。
*   使用 `SDO_NUM_RES` 参数时，`WHERE` 子句中不会使用任何其他条件。`SDO_NUM_RES` 仅考虑邻近性。例如，如果在 `WHERE` 子句中添加了一个标准，因为您希望最近的五个分支具有特定的邮政编码，而最近的五个分支中有四个分支具有不同的邮政编码，则上面的查询将返回一行。此行为特定于 `SDO_NUM_RES` 参数。在下面的查询中，您将为其他查询条件方案使用替代参数。

**使用距离确定距离达拉斯仓库最近的 5 个分支：**

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
    

![运行空间查询](images/query2.png) 备注：

*   `SDO_NN_DISTANCE` 运算符是 `SDO_NN` 运算符的辅助运算符；只能在 `SDO_NN` 运算符中使用。此运算符的参数是一个数字，它与指定为 `SDO_NN` 的最后一个参数的数字匹配；在此示例中为 1。这个论点没有隐藏的含义，它只是一个标签。如果指定了 `SDO_NN_DISTANCE()`，则可以按距离对结果进行排序，并保证返回的第一行是最接近的。如果要查询的数据以经度和纬度存储，则 `SDO_NN_DISTANCE` 的默认单位为米。
*   `SDO_NN` 运算符还具有一个 `UNIT` 参数，用于确定 `SDO_NN_DISTANCE` 返回的度量单位。
*   `ORDER BY DISTANCE` 子句可确保以顺序返回距离，并且首先返回最短的距离。

**确定距离达拉斯仓库最近的 5 个 WHOLESALE 分支：**

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
    

![运行空间查询](images/query3.png) 备注：

*   `SDO_BATCH_SIZE` 是可能影响查询性能的可调参数。`SDO_NN` 在内部一次计算该距离数。返回的最初一批行可能不满足 WHERE 子句中的约束条件，因此 `SDO_BATCH_SIZE` 指定的行数会不断返回，直到满足 WHERE 子句中的所有约束条件为止。您应该选择一个 `SDO_BATCH_SIZE`，它最初返回的行数可能满足 WHERE 子句中的约束条件。
*   `SDO_NN` 运算符中使用的 `UNIT` 参数指定 `SDO_NN_DISTANCE` 参数的度量单位。默认单位是与数据关联的单位。对于经度和纬度数据，默认值为米。
*   `B.BRANCH_TYPE = 'WHOLESALE' AND ROWNUM <= 5` 是 `WHERE` 子句中的附加约束条件。必须使用行号子句将返回的结果数限制为 5。
*   `ORDER BY DISTANCE_KM` 子句可确保以顺序返回距离，首先返回最短的距离，以英里为单位测量距离。

**识别休斯顿仓库 50 公里内的分支机构：**

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
    

![运行空间查询](images/query4.png) 备注：

*   `SDO_WITHIN_DISTANCE` 的第一个参数是要搜索的列。第二个参数是您要确定距离的位置。不应该对返回结果的顺序做出任何假设。例如，返回的第一行不能保证是最接近仓库 3 的客户。
*   `SDO_WITHIN_DISTANCE` 运算符中使用的 DISTANCE 参数指定距离值；在此示例中为 100。
*   `SDO_WITHIN_DISTANCE` 运算符中使用的 UNIT 参数指定 DISTANCE 参数的单位。默认单位是与数据关联的单位。对于经度和纬度数据，默认值为米；在此示例中为英里。

**标识距离为 50 公里的休斯顿仓库内的分行：**

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
    

![运行空间查询](images/query5.png) 备注：

*   `SDO_GEOM.SDO_DISTANCE` 函数计算分支位置与休斯顿仓库之间的距离。
*   `SDO_GEOM.SDO_DISTANCE` 的前 2 个参数是用于远程计算的 BRANCH 和 WAREHOUSE 位置。
*   `SDO_GEOM.SDO_DISTANCE` 的第三个参数是容差值。允差是 Oracle Spatial 使用的舍入错误值。经度和纬度数据的公差以米为单位。在本例中，公差为 50 mm。
*   `SDO_GEOM.SDO_DISTANCE` 参数中使用的 UNIT 参数指定 `SDO_GEOM`.`SDO_DISTANCE` 函数计算的距离的度量单位。默认单位是与数据关联的单位。对于经度和纬度数据，默认值为米。在本示例中为英里。
*   `ORDER BY DISTANCE_IN_MILES` 子句可确保以顺序返回距离，首先返回最短的距离，以英里为单位测量距离。

**确定沿海地区的分支：**

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
    

![运行空间查询](images/query6.png) 备注：

*   `SDO_ANYINTERACT` 运算符接受 2 个参数 geometry1 和 geometry2。对于 geometry1 在 geometry2 内部或边界上的行，运算符返回 `TRUE`。
*   在此示例中，geometry1 是 `B.GEOMETRY`，分支几何，geometry2 是 `C.GEOMETRY`，即沿海区域几何。COASTAL\_ZONE 表只有 1 行，因此不需要其他条件。

**确定沿海区外和 10 公里以内的分支：**

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
    

![运行空间查询](images/query7.png) 备注：

*   在此查询的第一部分，`SDO_WITHIN_DISTANCE` 运算符标识 COASTAL\_ZONE 10 公里以内的 BRANCHES。这包括 COASTAL\_ZONE 中的分支。
*   查询使用 `MINUS` 删除 COASTAL\_ZONE 内的 BRANCHES，仅将 BRACNCHES 留在 10 公里内和 COASTAL\_ZONE 之外。

## 了解详细信息

*   ［空间产品门户］ (https://oracle.com/goto/spatial)
*   [空间记录](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [空间博客](https://blogs.oracle.com/oraclespatial/)

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - Kamryn Vinson，2020 年 11 月