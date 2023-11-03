# 在 Cloud Shell 中创建 SSH 密钥

## 简介

要访问 Python 主机计算，您需要 SSH 密钥对。Oracle Cloud Infrastructure (OCI) Cloud Shell 是一个基于 Web 浏览器的终端，可通过 Oracle Cloud 控制台访问，从而访问 Linux shell。您将在 OCI Cloud Shell 中创建 SSH 密钥对。

估计的实验室时间：xx 分钟

### 目标

*   使用 OCI Cloud Shell 创建 SSH 密钥对。

### 先备条件

*   已登录到 OCI 控制台。

## 任务 1：创建 SSH 密钥对

1.  打开 cloud shell ![打开 Cloud Shell](images/sshkeys-01.png)
    
2.  当提示运行教程时，键入 N 并输入。 ![打开 Cloud Shell](images/sshkeys-02.png)
    
3.  在命令行中，运行以下每个命令来创建 SSK 密钥。
    
        <copy>
        mkdir ~/.ssh
        </copy>
        
    
          ```
        cd ~/.ssh \`\`\`
    
        <copy>
        ssh-keygen -b 2048 -t rsa -f my-ssh-key
        </copy>
        
    
    当提示输入口令短语时，可以单击 Enter 键而不输入口令短语，然后重复进行确认。  
    ![创建密钥](images/sshkeys-03.png)
    
4.  在命令行中，运行以下命令查看公钥。您将在后续步骤中使用此方法。
    
        <copy>
        cat ~/.ssh/my-ssh-key.pub
        </copy>
        
    
    ![查看公共密钥](images/sshkeys-04.png)
    
5.  单击折叠图标可最小化 Cloud Shell。
    
    ![折叠 Cloud Shell](images/sshkeys-05.png)
    
6.  观察 "Restore" 按钮以重新打开 Cloud Shell。您将在后续步骤中重新打开 Cloud Shell。
    
    ![还原 Cloud Shell](images/sshkeys-06.png)
    

现在，您可以**进入下一个练习**。

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - David Lapp，数据库产品管理，2023 年 6 月