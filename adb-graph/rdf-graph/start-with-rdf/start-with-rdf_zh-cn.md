# RDF 图形入门

## 简介

此实验室将指导您完成将 RDF 数据上载到将链接到 Autonomous Database 的存储桶的入门步骤。这需要从概要文件复制正确的 OCI 用户名。要允许 Graph Studio 访问 OCI 对象存储中的 RDF 数据（使用 DBMS\_CLOUD 程序包），您必须使用 OCI 账户创建访问令牌。这将在辅助实验室中使用。

估计时间：5 分钟

### 目标

*   将 RDF 数据上载到 OCI 对象存储
*   查看您的 OCI 用户名
*   生成访问标记

### 先备条件

此实验室假定您具有：

*   Oracle Cloud 帐户
*   使用此[链接](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)下载 MOVIESTREAM 文件 (moviestream\_rdf.nt)

## **任务 1：**将 RDF 数据上载到 OCI 对象存储

1.  使用您的 Oracle Cloud 身份证明登录 OCI 控制台。
2.  打开导航菜单，然后单击 "Storage"（存储）。在“Object Storage & Archive Storage（对象存储和归档存储）”下，单击“Buckets（存储桶）”，如下所示： ![图中介绍了从菜单中选择存储桶文件夹的位置](./images/buckets-folder.png)
3.  选择适用于您的 OCI 账户的区间。 ![图中显示了“区间”下拉菜单在“存储桶”页面上的位置](./images/compartment-menu.png)
4.  单击“Create Bucket（创建存储桶）”。此时将打开“创建存储桶”滑块，如下所示： ![图中介绍了“创建存储桶”页](./images/create-bucket.png)
5.  输入存储桶名称，将其他所有内容保留为默认值，然后单击“创建”。将创建存储桶，并在“存储桶”页上列出，如下所示： ![图中显示了创建存储桶的结果](./images/bucket-result.png)
6.  单击 RDF\_DATA\_BUCKET 链接并导航到“时段详细信息”页。

![图中显示了创建后的“存储桶”页](./images/bucket-page.png) 7. 在“Objects（对象）”部分中单击“Upload（上载）”。此时将打开“上载对象”滑块。 8. 选择本地系统上下载的 RDF moviestream\_rdf.nt 文件[链接](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)，然后单击“上载”。已成功上载文件。单击“关闭”返回“时段详细信息”页。上载的文件列在对象下方，如下所示： ![图中显示了上载到存储桶的对象](./images/image-upload.png)

1.  为上载的文件选择“Actions（操作）”菜单，然后单击“View Object Details（查看对象详细信息）”以访问上载的文件的属性。此时将打开“对象详细信息”滑块，如下所示： ![图中显示了突出显示了 "View Object Details"（查看对象详细信息）选项的 "Object Menu"（对象菜单）](./images/object-details.png)
2.  记下对象的 URL 路径。这用于 Graph Studio 中的 RDF 导入向导。 ![图中显示了在存储桶中查找对象的 URL 路径的位置](./images/url-path.png)

## **任务 2：**查看您的 OCI 用户名

1.  单击右上角的头像图标打开您的个人资料。Profile 下的第一个条目是您的 OCI 用户名。 ![图中显示了如何访问 OCI 配置文件](./images/oci-profile.png)
2.  记下您的 OCI 用户名。这用于 Graph Studio 中的 RDF 导入向导。 ![图中显示了用户详细信息中的 OCI 用户名](./images/oci-username.png)

## **任务 3：**从 OCI 控制台生成访问令牌

1.  使用您的 Oracle Cloud 身份证明登录 OCI 控制台。
    
2.  单击右上角的头像图标打开您的配置文件，然后单击“用户设置”。 ![图中显示了如何从配置文件访问用户设置](./images/user-settings.png)
    
3.  单击资源下的验证令牌，如下所示： ![图中显示了如何从用户设置的“资源”菜单访问验证令牌](./images/auth-tokens.png)
    
4.  单击“生成令牌”。此时将打开“生成标记”对话框。 ![图中显示了如何生成验证令牌](./images/gen-tokens.png)
    
5.  输入说明并单击“生成令牌”。生成的令牌详细信息如下所示： ![图中显示了如何复制生成的验证令牌](./images/token-details.png)
    
6.  单击“复制”以复制标记并保存以供以后使用。
    

这个实验室结束了。_现在，您可以继续下一个练习。_

## 确认

*   **作者** - 杰出产品经理 Melliyal Annamalai
*   **技术贡献者** - 圣莫尼卡专家中心 Nicholas Cusato
*   **上次更新者/日期** - Nicholas Cusato，Santa Monica Specialist Hub，2022 年 2 月 25 日