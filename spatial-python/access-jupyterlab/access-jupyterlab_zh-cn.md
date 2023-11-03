# 访问 JupyterLab

## 简介

笔记本是用于代码、说明性文本和可视化的交互式文档。在本研讨会中，您将使用开源 JupyterLab，它提供了一个基于 Web 的笔记本环境，其中包含许多用户友好的功能，例如文件上载。

估计的实验室时间：5 分钟

### 目标

*   验证对 JupyterLab 的访问权限
*   浏览记事本功能
*   选择用于执行剩余动手实验室的选项

## 任务 1：检索 JupyterLab 的 IP 地址

1.  从主菜单中，导航到“Compute（计算）”>“Instances（实例）”

![检索 IP 地址](images/compute-01.png)

2.  在研讨会说明页面中，单击左上角的**查看登录信息**，然后复制区间名称。

![检索 IP 地址](images/compartment.png)

1.  在 OCI 控制台中，粘贴区间名称，然后从下拉列表中选择。

![检索 IP 地址](images/compute-02.png)

4.  请注意计算实例的公共 IP。已在此实例上设置 JupyerLab。您稍后将在此实验室和其他实验室中使用此功能。

![检索 IP 地址](images/compute-03.png)

## 任务 2：验证对 JupyterLab 的访问权限

1.  打开新的浏览器选项卡并输入 URL **http：//\[IP address\]：8001/lab** ，其中 \[IP address\] 是任务 1 中检索到的地址。
    
    ![访问 JupyterLab](images/access-jupyter-01.png)
    
2.  输入密码 **livelabs** ，然后单击**登录**。
    

## 任务 2：浏览 Jupyter 笔记本

Jupyter Notebook 是一个基于 Web 的交互式工具，允许您创建和共享包含实时代码、方程式、可视化和文本的文档。它在数据科学界广泛用于原型设计和数据分析。

在本任务中，我们将介绍使用 Jupyter Notebook 的基本知识。

1.  创建新笔记本。
    
    当 Jupyter 环境加载时，您应该看到启动器选项卡已打开。
    
    ![启动器选项卡已打开](./images/launcher1.png)
    
    如果未看到启动器窗口，请选择窗口左上角的文件，然后选择“新建启动器”。
    
    ![打开新的启动器选项卡](./images/launcher2.png)
    
    在启动器窗口中，选择 "Python 3" 以使用 Python 编程语言创建新笔记本。将创建一个新的笔记本，您可以通过在代码单元格中输入代码或在减价单元格中添加减价文本来开始处理它。
    
    ![创建新的 Python 笔记本](./images/launcher3.png)
    
2.  添加一些减价文本。
    
    单击代码单元格并使用单元格类型下拉列表选择 'Markdown'
    
    ![添加减价单元格](./images/notebook1.png)
    
    将以下内容粘贴到单元格中并单击工具栏上的播放按钮，或按 Shift+Enter 运行单元格。
    
        	<copy>
        	# My First Notebook
        	This is my first Jupyter notebook
        	</copy>
        
    
    ![减价的结果](./images/notebook2.png)
    
3.  编写一些 Python 代码。将以下内容粘贴到下一个单元格并运行它。“Hello，World！（您好，世界！）”应出现在单元格下方。
    
        	<copy>
        	print('Hello, World!')
        	</copy>
        
        
    
    ![大家好](./images/notebook3.png)
    
4.  要保存 Jupyter Notebook，请单击工具栏上的“保存”图标，或按 Ctrl+S（或按 macOS 上的 Cmd+S）。笔记本将使用 .ipynb 文件扩展名进行保存。
    

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **贡献者** - Rahul Tasker、Denise Myrick、Ramu Gutierrez
*   **上次更新者/日期** - David Lapp，2023 年 8 月