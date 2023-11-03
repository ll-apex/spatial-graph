# 纳入空间分析

## 简介

在此实验室中，您将结合空间分析来增强上一实验室的地图。您将配置搜索位于所选状态的用户定义距离内的机场。

估计的实验室时间：30 分钟

### 目标

*   了解基本空间分析操作
*   了解空间分析与 APEX 映射区域的集成

### 先备条件

*   实验 3：从头开始创建映射

## 任务 1：为筛选器添加区域

1.  单击左侧树顶部的**第 3 页：机场和国家/地区地图**。然后，在右侧的“页属性”面板中，“外观”下的“页模板”将更改为**左侧列**。
    
    ![更新页面模板](images/add-spatial-analysis-01a.png)
    
    然后，您应在布局中看到 **LEFT COLUMN** 。
    
    ![更新页面模板](images/add-spatial-analysis-01b.png)
    
2.  将静态内容区域拖到左侧列。
    
    ![添加静态内容区域](images/add-spatial-analysis-01c.png)
    
3.  重命名为**我的筛选器区域**或您选择的名称。
    
    ![重命名区域](images/add-spatial-analysis-02.png)
    

## 任务 2：添加用于状态选择的项

1.  将 "Select List"（选择列表）项拖动到过滤器区域，并将名称更新为 **P3\_STATE** 。
    
    ![添加选择列表项](images/add-spatial-analysis-03.png)
    
2.  在右侧的“Page Item（页项）”属性中，向下滚动到“List of Values（值列表）”部分。使用切换启用**必需值**，将类型设置为 **SQL 查询**并输入以下查询：
    
        <copy>
          select name, state_code
            from EBA_SAMPLE_MAP_SIMPLE_STATES
        order by name
        </copy>
        
    
    ![SELECT 查询](images/add-spatial-analysis-04.png)
    
3.  在右侧的“Page Item( 页项 )”属性中 , 向下滚动到“Default( 默认 )”区域。将 "Type”（类型）设置为 **Static（静态）**，将值设置为 **'Texas'** 或您选择的另一个状态（用单引号括起）。
    
    ![配置选择列表](images/add-spatial-analysis-05.png)
    

## 任务 3：为距离条目添加项目

1.  将数字字段拖动到筛选器区域中。将名称更新为 **P3\_DISTANCE** ，将标签更新为 **Proximity (km)** 。
    
    ![添加数字字段项](images/add-spatial-analysis-06.png)
    
2.  在右侧的“页项”属性中，向下滚动到“验证”部分并启用**必需的值**。
    
    ![将验证设置为“必需值”](images/add-spatial-analysis-07.png)
    
3.  向下滚动到“Default( 默认 )”区域。将 ”Type"（类型）设置为 **Static** ，将值设置为 **100** 。
    
    ![设置默认值](images/add-spatial-analysis-08.png)
    
    现在，您有按邻近状态过滤机场的输入。下一步，使用动态操作应用筛选器。
    

## 任务 4：使用动态操作应用筛选器

接下来，创建用户更改状态和/或距离值时调用的操作。

1.  右键单击 P3\_STATE 或 P3\_DISTANCE 项，然后选择**创建动态操作**（我们创建的操作将应用于这两个项）。
    
    ![创建动态操作](images/add-spatial-analysis-09.png)
    
2.  在右侧的“动态操作”属性中，将“名称”设置为**验证和刷新**。在“时间”部分下，将“事件”设置为**更改**，“选择类型”设置为**项**，将项设置为以逗号分隔的列表 **P3\_DISTANCE，P3\_STATE** 。请注意，项文本框右侧的按钮允许您从列表中选择项。要防止提交距离的负值，请在“客户端条件”部分下，将“类型”设置为**项目 >= 值**，将项目设置为 **P3\_DISTANCE** ，将“值”设置为 **0** 。
    
    ![配置动态操作](images/add-spatial-analysis-10.png)
    
3.  动态操作配置有 TRUE 操作和 FALSE 操作，这些操作根据已配置的条件调用。在这种情况下，客户端条件 (P3\_DISTANCE >= 0) 确定是调用 TRUE 操作（满足条件）还是 FALSE 操作（不满足条件）。这将允许我们捕获负距离输入。
    
    当客户端条件为 TRUE 时，操作应提交输入值并刷新页面。单击“True( 真 )”下的操作。在右侧的 ”Action“( 操作 ) 属性中 , 在 ”Identification“( 标识 ) 设置下 ”Action"（操作）设置为 **Refresh（刷新）**。在“受影响的元素”下，将“选择类型”设置为**区域**，将“区域”设置为**“我的映射区域”**（或您使用的名称（如果不同）。请在左侧页面树中观察“真”操作更改为“刷新”。
    
    ![配置动态操作](images/add-spatial-analysis-11.png)
    
4.  下一步，将操作配置为在不满足客户端条件时调用，这意味着输入了负距离值。在任一项的“动态操作”下，右键单击 False 并选择**创建 FALSE 操作**。
    
    ![配置动态操作](images/add-spatial-analysis-12.png)
    
5.  距离为负时调用的 FALSE 操作将成为用户的弹出消息。单击“False”操作。在右侧的 ”Action“( 操作 ) 属性中 , 在 ”Identification“( 标识 ) 下 , 将 ”Action“( 操作 ) 设置为 **Alert( 警报 )** 。在“设置”下 , 将“标题”设置为**无效距离** ( 这将是预警横幅 ), 将“消息”设置为**距离必须 >= 0** ( 这将是预警正文 )。在左侧的页面树中观察 ”False“ 操作更改为 ”Alert”。
    
    ![配置动态操作](images/add-spatial-analysis-13.png)
    
6.  您的地图区域当前包含一个显示所有状态的状态层。现在，您可以调整此层以仅显示从 P3\_STATE 菜单中选择的状态。在左侧的页面树中，在“图层”下单击“状态”。在右侧的层属性中 , 在 "Identification”（标识）下将 "Name"（名称）更改为 **Selected State** 。在 "Source"（源）下，将 Where 子句设置为 **state\_code = ：P3\_STATE** 。观察左侧页面树中层名称更改为“选定状态”。
    
        <copy>
        state_code = :P3_STATE
        </copy>
        
    
    ![配置 WHERE 子句](images/add-spatial-analysis-14.png)
    
7.  最后，更新 Airports 层以返回按用户指定的状态和邻近度过滤的项。在左侧的 Page 树中，单击 Airports 层。在右侧“源”下的“层”属性中，将“类型”更改为 **SQL 查询**。对于 SQL 查询，请输入使用 Oracle Database 的本机 SQL“距离内”运算符的以下内容。
    
        <copy>
        select a.*
          from EBA_SAMPLE_MAP_AIRPORTS a,
               EBA_SAMPLE_MAP_SIMPLE_STATES b
         where b.state_code= :P3_STATE
           and a.land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance='|| :P3_DISTANCE ||' unit=KM') = 'TRUE'
        </copy>
        
    
    要提交页项，请输入逗号分隔的列表 **P3\_STATE，P3\_DISTANCE** 。
    
    ![空间 SQL 查询](images/add-spatial-analysis-15.png)
    
8.  您的页面已准备好查看。单击**保存**，然后单击右上角的绿色**运行**按钮。呈现页面后，选择 **Alabama** 作为状态。该地图显示 100 公里（默认距离）内的选定州和机场。
    
    ![保存并运行页](images/add-spatial-analysis-16.png)
    
9.  将所选状态更改为 **Kansas** 。观察地图现在显示选定的州和机场 100 公里。
    
    ![选择堪萨斯州](images/add-spatial-analysis-17.png)
    
10.  将距离增加到 600 公里，然后单击 Enter 或 Tab 提交。观察地图现在显示距离较远的其他机场。
    
    ![将距离增加到 600 公里](images/add-spatial-analysis-18.png)
    
11.  最后，确认提交负距离会导致我们之前配置的错误弹出窗口。
    
    ![负距离警报](images/add-spatial-analysis-19.png)
    
    如您在本研讨会开始时安装的示例映射应用程序中所示，可以使用映射区域和空间实现大量附加功能。本研讨会介绍了基础知识，我们希望您的兴趣得到激发，并且您将在 APEX 应用程序中利用地图和空间分析的强大功能。
    

## 了解详细信息

*   [Oracle Spatial](https://www.oracle.com/database/spatial/)
*   [APEX](https://apex.oracle.com/)

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - David Lapp，数据库产品管理，2023 年 3 月