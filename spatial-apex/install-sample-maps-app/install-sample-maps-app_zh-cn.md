# 安装示例映射应用程序

## 简介

通过 Oracle APEX，您可以访问一系列示例应用，这些应用可以突出显示特定功能领域。其中有一个示例映射应用程序展示了 Oracle APEX 中的映射功能。提供了各种示例，作为功能示例和进一步定制的起点。在此实验室中，您将安装并配置示例映射应用程序。

估计的实验室时间：15 分钟

### 目标

*   安装示例映射应用程序
*   加载支持数据

### 先备条件

*   需要 Oracle APEX 21.1+。本研讨会中的屏幕截图使用 APEX 21.2 进行。由于我们通常建议使用[最新版本的 APEX](https://www.oracle.com/tools/downloads/apex-downloads/) ，因此用户界面中偶尔会出现较小的差异。

## 任务 1：安装应用程序

1.  首先单击**应用程序构建器**。
    
    ![APEX Application Builder（APEX 应用程序构建器）](images/install-sample-maps-00.png)
    
2.  单击 **Install a Starter or Sample App** 。
    
    ![选择启动应用程序或示例应用程序](images/install-sample-maps-01.png)
    
    **注：**如果工作区具有现有应用程序，则依次单击**创建**和**启动应用程序**。
    
3.  单击**示例**可打开新的浏览器选项卡，其中包含可用示例应用程序的列表。
    
    ![选择样品](images/install-sample-maps-02.png)
    
4.  向下滚动到**示例映射**，然后单击**下载应用程序**。
    
    ![图像替代文本](images/install-sample-maps-03.png)
    
    系统会提示您将应用程序包保存到本地文件夹。
    
    **注：**如果您重定向到 github，请导航到 APEX 版本的文件夹并下载 **sample-maps.zip** 。
    
5.  返回应用程序构建器浏览器选项卡 a. 并单击**导入**。
    
    ![选择导入](images/install-sample-maps-04.png)
    
6.  拖放或浏览到以前下载的示例映射应用程序 zip 文件。将“文件类型”选择保留为“数据库应用程序”，然后单击**下一步**。
    
    ![选择示例映射应用程序 zip](images/install-sample-maps-05.png)
    
7.  文件导入已确认。再次单击**下一步**。
    
    ![单击“下一步”](images/install-sample-maps-06.png)
    
8.  保留默认菜单选择，然后单击**安装应用程序**。
    
    ![单击“安装应用程序”](images/install-sample-maps-07.png)
    
    这将转到“Install Application（安装应用程序）”向导。
    
9.  保留默认菜单选择，然后单击**下一步**。
    
    ![单击“下一步”](images/install-sample-maps-08.png)
    
10.  单击**下一步**以验证系统兼容性。
    

![单击“下一步”](images/install-sample-maps-09.png)

11.  在确认兼容性后，单击**安装**启动支持数据库对象和 APEX 应用程序的安装。

![单击“安装”](images/install-sample-maps-10.png)

12.  安装完成后，单击**运行应用程序**。

![单击“运行应用程序”](images/install-sample-maps-11.png)

13.  使用 APEX 工作区用户名和密码登录到示例映射应用程序。

![登录](images/install-sample-maps-12.png)

## 任务 2：加载数据

1.  您现在位于示例映射应用程序中，其中提供了大量 APEX 中的映射和空间操作的示例。在初始启动时，将显示有关数据加载的警告消息。单击该消息中的**数据加载**链接。您将导航到完成演示数据加载的页面。
    
    ![单击“Data Loading（数据加载）”](images/install-sample-maps-13.png)
    
2.  “数据加载”页显示示例映射应用程序和本研讨会其余部分使用的状态和机场数据集的加载状态。安装示例映射应用程序时，这些数据集仅部分加载。要完成示例数据加载，您可以直接从存储在 github 中的文件加载，也可以先下载文件并从本地系统加载。如果您在需要代理才能访问 github 的网络中运行 APEX，则应使用后一种选项。
    
    如果您的 APEX 实例不需要代理来访问 github（例如，apex.oracle.com 或 APEX wth Oracle Autonomous Database），则单击该按钮以**直接从 GitHub** 加载，然后单击右上方的**加载数据集**。
    
    ![点击直接从 Github](images/install-sample-maps-14.png)
    
    如果 APEX 实例需要代理才能访问 github（例如，在公司防火墙后运行的 APEX），或者直接从 github 加载其他问题，请单击**上载文件**按钮以提供替代说明。
    
3.  数据加载完成后，您将在右上角看到一条通知，警告消息将消失。示例映射应用程序现在可供使用。
    
    ![数据加载确认](images/install-sample-maps-15.png)
    

## 任务 3：浏览示例映射应用程序

1.  单击任何磁贴将导航到应用程序中的关联页面。例如，单击**映射和报表**。
    
    ![定位至“映射和报表”页](images/install-sample-maps-16.png)
    
2.  在此页面中，单击地图中右侧项目上报表中的项目，然后打开信息窗口。单击左上角的图标将打开导航面板以访问应用程序中的其他页面。
    
    ![与地图交互](images/install-sample-maps-17.png)
    
3.  单击导航面板中的项可访问应用程序中的其他页面。
    
    !["Navigation"（导航）面板显示其他页面](images/install-sample-maps-18.png)
    
4.  要关闭导航面板，请单击左上角的图标。您还可以通过单击左上方的**示例映射**导航到应用程序主页。
    
    ![关闭导航面板](images/install-sample-maps-19.png)
    

## 任务 4：浏览演示数据

1.  返回到 APEX，依次单击 **SQL Workshop（SQL 工作室）**和 **Object Browser（对象浏览器）**。
    
    ![SQL 工作室 - 对象浏览器](images/install-sample-maps-20.png)
    
2.  观察之前执行的数据加载步骤创建的表。单击 **EBA\_SAMPLE\_MAP\_AIRPORTS** 。请注意，这些列包括类型为 SDO\_GEOMETRY（Oracle 本机空间数据类型）的名为 GEOMETRY 的列。
    
    ![具有本机几何列的表](images/install-sample-maps-21.png)
    
3.  单击**数据**选项卡可查看表内容。
    
    ![表内容](images/install-sample-maps-22.png)
    
    然后向右滚动以查看几何列。由于机场存储为点，因此 APEX 将显示点几何值的字符串表示形式。积分始终基于单个坐标，因此 APEX 以这种方式显示值很有意义。
    
    ![点几何结构](images/install-sample-maps-23.png)
    
4.  单击 **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES** 。同样，请注意，这些列包括一个名为 GEOMETRY 的列，该列类型为 SDO\_GEOMETRY（Oracle 的本机空间数据类型）。
    
    ![具有本机几何列的表](images/install-sample-maps-24.png)
    
5.  单击**数据**选项卡以查看表内容。由于此表存储状态，因此几何图形是多边形。APEX 不显示这些值的字符串表示形式，因为它们可能包含非常长的一组坐标。
    
    ![多边形几何结构](images/install-sample-maps-25.png)
    
6.  观察名为 **MDRT\_....$** 的表。这些索引由数据库在后台自动创建和管理，以支持其他表上的空间索引。从不手动创建、更新或删除这些表。它们仅用于支持空间分析操作，可以忽略。
    
    ![空间索引构件](images/install-sample-maps-26.png)
    
7.  最后，可以使用此数据运行基本空间查询。单击 **SQL Workshop（SQL 工作室）**，然后单击 **SQL Commands（SQL 命令）**。
    
    ![SQL 工作室 - SQL 命令](images/install-sample-maps-27.png)
    
8.  以下查询返回占地面积超过 1000 英亩、距离德克萨斯州 100 公里的机场数量。请注意使用本机空间运算符 **sdo\_within\_distance** 。将查询复制并粘贴到“SQL Commands（SQL 命令）”窗口中，然后单击右上方的**运行**。
    
        <copy>
        select count(a.id) as number_of_airports
        from EBA_SAMPLE_MAP_AIRPORTS a,
              EBA_SAMPLE_MAP_SIMPLE_STATES b
        where b.state_code= 'TX'
           and land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance=100 unit=KM') = 'TRUE'
        </copy>
        
    
    ![空间查询](images/install-sample-maps-28.png)
    
9.  在 sdo\_within\_distance 运算符中，将距离更新为 300 公里，然后重新运行。根据较大的搜索区域观察结果更改。
    
    ![空间查询](images/install-sample-maps-29.png)
    

在后面的练习中，您将配置一个映射，用于显示此查询的结果，其中状态和距离由页面中的菜单控制。

您现在已安装并浏览了示例映射应用程序和数据。接下来，您将开始创建自己的应用程序和映射。

实验室结束了。现在，您可以进入下一个实验室。

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **贡献者** - Oracle APEX 开发部门 Carsten Czarski
*   **上次更新者/日期** - David Lapp，数据库产品管理，2023 年 3 月