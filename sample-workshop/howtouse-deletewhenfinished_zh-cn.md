# 单一实验室的研讨会

## 说明 - 完成后删除此文件

1.  在 Atom 或 Visual Studio Code 中打开示例研讨会模板
2.  我们预先创建了 5 个文件夹。研讨会由多个实验室组成。
3.  删除如下备注：_列出此实验室的目标_
4.  确保对空格使用小写文件夹、文件名和短划线 (setup-adb NOT Setup\_ADB)
5.  您的映像名称应具有描述性名称。不仅 adb1、adb2、adb3。为了实现无障碍访问，我们需要图像描述来解释图像的外观。请记住所有小写和短划线。
6.  从 WMS 下载我们的 QA 文档。我们发现，当您知道前期搬到生产中需要什么并且您使用骨架时，车间可以更快地投入生产。

PS：不需要 Readme.md。自述文件仅存在于顶级磁带库级别。由于无法跟踪 GitHub 上的使用情况，因此会将所有流量定向到 LiveLabs。不要创建任何指向 GitHub 的直接链接，您的研讨会可能非常受欢迎，但我们无法跟踪它，因此没有人会知道。

## Oracle Cloud 菜单导航的绝对路径

**练习 1：预配实例 -> 步骤 0：使用这些标准化的图片进行 Oracle Cloud 导航（仅用于预配）** - 我们包括用于导航 Oracle Cloud 菜单的常用屏幕截图列表。请阅读本节，并酌情使用相关的绝对路径图像。在 Oracle Cloud 用户界面更新时，这将在未来证明您的研讨会。

## 文件夹结构

在本例中，目标是从一个较长的“父母”研讨会创建多个“儿童”研讨会。子项由父项中的部分组成。

示例 - 研讨会/ -- 个别实验室

        provision/
        setup/
        dataload/
        query/
        introduction/
          introduction.md       -- description of the everything workshop, note that it is a "lab" since there is only one
    
    workshops/
       freetier/                -- freetier version of the workshop
        index.html
        manifest.json
       livelabs/                -- livelabs version of the workshop
        index.html
        manifest.json
    

### FreeTier 与 LiveLabs

*   "FreeTier" - 包括免费试用、付费账户以及一些研讨会的“始终免费”账户（棕色按钮）
*   "LiveLabs" - 这些是使用 Oracle 提供的租户（绿色按钮）的研讨会
*   "Desktop"（桌面）- 这是新部署，其中的研习会封装在计算实例中运行的 NoVNC 环境中

### 关于研讨会

研讨会将所有 6 个单独的实验室按顺序排列。

文件夹结构包括简介“实验室”，该实验室将研讨会描述为一组完整的 6 个实验室。注意：您可能不需要对每个工作坊的父版本和子版本进行不同的介绍，这只是说明性的。

查看 product-name-workshop/freetier 文件夹并查看 manifest.json 文件以查看结构。

> **注：**在标题中使用 "Lab n:" 是可选的

先决条件 "lab" 是 oracle-livelabs/公用资料档案库上公用文件夹中的第一个实验室。因为这个实验室已经存在，所以我们可以改用 RAW/绝对 URL：

    "filename": "https://oracle-livelabs.github.io/common/labs/cloud-login/cloud-login-livelabs2.md"        },
    

manifest.json 文件需要知道每个实验室相对于其存在于层次结构中的位置的位置。在此结构中，实验室分为两层，例如：

    "filename": "../../provision/provision.md"
    

### 例如：

本 [APEX Workshop（APEX 研讨会）](https://oracle-livelabs.github.io/apex/spreadsheet/workshops/freetier/)是一个具有一组实验室的研讨会示例：[https://github.com/oracle-livelabs/apex/tree/main/spreadsheet](https://github.com/oracle-livelabs/apex/tree/main/spreadsheet) 。