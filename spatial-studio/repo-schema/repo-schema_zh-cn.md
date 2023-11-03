# Spatial Studio 资料档案库的数据库用户

## 简介

此练习介绍如何创建要用于 Spatial Studio 元数据资料档案库的数据库方案。这是用于存储 Spatial Studio 中所做工作的方案，例如数据集、分析和项目的定义。

Spatial Studio 资料档案库的数据库方案在技术上可以具有任何名称。为了与其他 Spatial Studio 工作室保持一致，我们将用户名命名为 **studio\_repo** 。请注意，这是一个数据库用户名，与 Spatial Studio 应用程序用户名不同，例如安装 Spatial Studio 应用程序本身时创建的默认 Spatial Studio 管理员用户名 (studio\_admin)。

估计的实验室时间：5 分钟

### 目标

*   了解如何为 Spatial Studio 元数据资料档案库创建方案
*   了解如何下载用于数据库连接的 Wallet

### 先备条件

*   Oracle Free Tier，Always Free，Paid 或 LiveLabs Cloud 账户
*   访问数据库 SQL Developer Web。

## 任务 1：创建资料档案库方案

1.  在 SQL Developer Web 中，以 **admin** 用户身份连接到要用于 Spatial Studio 资料档案库的自治数据库
    
2.  为 Spatial Studio 资料档案库创建方案。方案可以具有任何名称，但为了与其他实验室保持一致，我们使用名称 **studio\_repo** 。Oracle Autonomous Database 的密码要求位于[此处](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/manage-users-create.html#GUID-72DFAF2A-C4C3-4FAC-A75B-846CC6EDBA3F)。记下您选择的密码，我们将在后面的步骤中使用它。
    
        <copy>CREATE USER studio_repo
        IDENTIFIED BY <password goes here>;</copy>
        

## 任务 2：分配表空间限额

1.  将默认表空间分配给 Spatial Studio 资料档案库方案。使用 Autonomous Database，您可以使用表空间名称**数据**
    
        <copy>ALTER USER studio_repo
        DEFAULT TABLESPACE data;</copy>
        
2.  将表空间限额分配给 Spatial Studio 资料档案库方案。Spatial Studio 的元数据占用非常少的存储空间。因此，限额主要用于存储资料档案库方案中的业务数据。对于此实验室，配额值 **250M** 正常。如果要试验其他数据集，还可以将该值设置为 **unlimited** 。
    
        <copy>ALTER USER studio_repo
        QUOTA <quota value> ON data;</copy>
        

## 任务 3：授予权限

1.  向 Spatial Studio 资料档案库方案用户授予以下权限
    
        <copy>
        GRANT CONNECT,
              CREATE SESSION,
              CREATE TABLE,
              CREATE VIEW,
              CREATE SEQUENCE,
              CREATE PROCEDURE,
              CREATE SYNONYM,
              CREATE TYPE,
              CREATE TRIGGER
        TO  studio_repo
        </copy>
        

studio\_repo 方案现在可以用作 Spatial Studio 资料档案库。

## 任务 4：下载 Wallet

Spatial Studio 需要 Wallet 才能连接到我们创建的 Autonomous Database 资料档案库方案。我们将在下一个实验室使用钱包。

1.  导航到 Autonomous Database，然后选择“View Details（查看详细信息）”
    
    ![图像替代文本](images/repo-schema-1.png "图像标题")
    
2.  选择“DB Connection（数据库连接）”选项卡
    
    ![图像替代文本](images/repo-schema-2.png "图像标题")
    
3.  点击下载钱包 . . 。 ![图像替代文本](images/repo-schema-3.png "图像标题")
    
    系统将提示您输入 Wallet 文件的密码。Wallet 是单个 zip 文件。
    
4.  将 Wallet 文件保存到方便的位置。您需要在下一个实验室中使用此文件。
    

现在，您可以[进入下一个练习](#next)。

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - David Lapp，数据库产品管理，2023 年 3 月