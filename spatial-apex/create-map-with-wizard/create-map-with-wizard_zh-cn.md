# 使用向导创建映射

## 简介

Oracle APEX 提供了用于创建各种有用页面类型的向导。在此练习中，您将使用向导创建一个新应用程序和一个包含地图的页面。然后检查生成的页面以了解“地图区域”。

估计的实验室时间：10 分钟

### 目标

*   了解 APEX 映射区域的基础知识

### 先备条件

*   完成实验室 1：安装示例映射应用程序

## 任务 1：使用向导创建具有映射页的新应用程序

向导提供了一种快速简便的方法来创建新应用程序和第一个映射。

1.  导航到**应用程序构建器**，然后单击**创建**。 ![在应用程序构建器中创建应用程序向导](images/create-map-01.png)
    
2.  选择**新建应用程序**。 ![创建应用程序 - 新建应用程序](images/create-map-02.png)
    
3.  输入应用程序的名称，然后单击**添加页**。 ![创建申请 - 表单](images/create-map-03.png)
    
4.  选择**映射**作为页面类型。 ![创建应用程序 - 添加页](images/create-map-04.png)
    
    **注**：此向导与在现有应用程序中使用**创建页**相同。
    
5.  输入**机场地图**作为页名。（通过此向导，页名还将用作在该页中创建的地图区域的名称。）单击表输入右侧的图标以选择 **EBA\_SAMPLE\_MAP\_AIRPORTS** 表。对于几何列，选择 **GEOMETRY** ，最后选择将鼠标悬停在映射中的项上时要使用的工具提示的列。 ![“创建应用程序 - 创建映射”页](images/create-map-05.png)
    
6.  请注意，您的新页面现在列在**页面**下。单击**创建应用程序**。 ![创建应用程序 - 完成创建应用程序](images/create-map-06.png)
    
7.  您将导航到管理新应用程序的页面。单击**运行应用程序**。 ![运行应用程序](images/create-map-07.png)
    
8.  使用 APEX 登录用户名和密码登录应用程序。 ![登录您的应用程序](images/create-map-08.png)
    
9.  我们为应用程序选择的默认布局提供了一个主页，其中包含指向其他页面的链接。从主页中，导航到刚刚创建的页面。 ![“应用程序”主页](images/create-map-09.png)
    
10.  观察该页面包括一个交互式地图，其中显示您配置的机场位置和工具提示。 ![查看映射](images/create-map-10.png)
    

## 任务 2：检查映射页

现在，您将检查向导创建的地图区域。

1.  在页面底部的开发人员工具栏中，单击**第 2 页**按钮以编辑该页面。 ![编辑页面](images/create-map-11.png)
    
2.  在左侧的页树中，在**正文**下，单击**机场地图**。这是由“创建页”向导创建的映射区域的标题。默认情况下，它与页面标题相同，可以根据需要进行更改。在右侧的“区域详细信息”面板中，请注意此区域的类型为**映射**。 ![视图页面属性](images/create-map-12.png)
    
3.  映射区域包括作为点、线和多边形（来自 Oracle Spatial、GeoJSON 或坐标）的层，这些层显示在背景地图上。步入“创建页”向导时，使用表 EBA\_SAMPLE\_MAP\_AIRPORTS 中的 GEOMETRY 列（即 Oracle Spatial 数据）选择了映射。因此，向导创建了一个包含这些机场位置的层。默认情况下，层与页具有相同的名称，即**机场地图**。这可以根据需要进行更改。
    
    要检查此层，请在左侧面板的页树中，在“层”下单击**机场地图**。配置详细信息显示在右侧的**层**面板中。有关配置项的信息，请单击中间面板中的**帮助**选项卡。单击配置项后，将显示该项的帮助信息。例如，单击**层类型**菜单以查看有关其选项的帮助。 ![检查地图层属性](images/create-map-13.png)
    
4.  在 "Layer"（层）面板中向下滚动以查看向导设置的其他配置选项，包括设置了几何数据类型的列映射。在此处，您使用的是 Oracle 的本机空间数据类型 SDO\_GEOMETRY，列名是 GEOMETRY。 ![检查地图层属性](images/create-map-14.png)
    

祝贺你创建你的第一个地图。除了你刚刚探索的基本知识之外，还有很多能力。随意尝试对参数进行调整，然后保存并运行以查看结果。在下一个实验室中，您将从头开始配置新的地图区域。

实验室结束了。现在，您可以进入下一个实验室。

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - David Lapp，数据库产品管理，2023 年 3 月