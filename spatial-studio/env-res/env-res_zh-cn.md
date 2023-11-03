# 访问 Spatial Studio

## 简介

此练习将介绍从 Oracle LiveLabs 保留访问 Oracle Spatial Studio (Spatial Studio) 的过程。您的环境包括 Spatial Studio 和 Autonomous Database。首次登录 Spatial Studio 时，您将提供 Autonomous Database 的连接信息。

估计的实验室时间：10 分钟

### 目标

在此实验室中，您将：

*   下载适用于 Autonomous Database 的 Cloud Wallet
*   执行首次登录 Spatial Studio 以提供 Autonomous Database 连接信息

### 先备条件

*   “Oracle Spatial Studio 简介”的已完成 LiveLabs 保留

## 任务 1：下载适用于 Autonomous Database 的 Cloud Wallet

1.  在 Workshop Details 中，记下您的 Cloud 用户名、密码、区间和 Spatial Studio IP 地址。然后启动云控制台。

![图像替代文本](images/1-1.png "图像标题")

2.  使用您的云用户名和初始密码通过 **Oracle Cloud Infrastructure Direct Sign-in** 登录。系统将提示您更改默认密码。

![图像替代文本](images/1-2.png "图像标题")

3.  依次导航到 **Oracle Database** 和 **Autonomous Database** 。

![图像替代文本](images/1-3.png "图像标题")

4.  在左侧的区间表单中，开始键入之前注明的区间名称。这将动态筛选“区间”列表。列出后，选择您的区间。随后将列出您的 Autonomous Database。单击指向 Autonomous Database 的链接。

![图像替代文本](images/1-4.png "图像标题")

5.  单击**数据库连接**，然后单击**下载 Wallet** 。您将提升为 wallet 密码。输入任何字符串，因为将不会使用此密码。将钱包保存到笔记本电脑上方便的位置，因为您将在下一步使用它。

![图像替代文本](images/1-5.png "图像标题")

## 任务 2:Spatial Studio 首次登录

1.  现在，您将使用之前注明的 Spatial Studio IP 地址。在浏览器中打开新选项卡并导航到 **https：//\[your Spatial Studio IP address\]：4040/spatialstudio** 。例如，如果您的 Spatial Studio IP 地址为 123.123.12.123，则您将导航到 https://123.123.12.123:4040/spatialstudio.，因为您的 Spatial Studio 实例未配置签名 SSL 证书，您将看到特定于浏览器的安全警告。接受警告并转到站点。在生产环境中，将配置证书，不会发生这种情况。使用用户 **admin** 和密码 **welcome1** 登录。

![图像替代文本](images/2-1.png "图像标题")

2.  首次登录 Spatial Studio 会提示您输入 Spatial Studio 元数据资料档案库的数据库连接信息。依次单击 **Autonomous Database** 和**下一步**。在下一个 scren 上，拖放之前下载的 wallet 文件，然后单击**确定**。

![图像替代文本](images/2-2.png "图像标题")

3.  现在会提示您输入自动数据库连接信息。输入用户 **studio\_repo** ，密码 **Welcome1Welcome1** ，然后选择中等服务级别。

![图像替代文本](images/2-3.png "图像标题")

Spatial Studio 现在正在 Autonomous Database 中构建其元数据表。这将需要大约 30 秒。

4.  当 Spatial Studio 打开时，首次登录即完成，您可以继续参加研讨会。

![图像替代文本](images/2-4.png "图像标题")

现在，您可以[进入下一个练习](#next)。

## 了解详细信息

*   [Spatial Studio 产品页面](https://oracle.com/goto/spatialstudio)

## 确认

*   **作者** - 数据库产品管理 David Lapp
*   **上次更新者/日期** - David Lapp，数据库产品管理，2021 年 6 月