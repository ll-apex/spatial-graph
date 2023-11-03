# クラウド・シェルでのSSHキーの作成

## 概要

Pythonホスト・コンピュートにアクセスするには、SSHキー・ペアが必要です。Oracle Cloud Infrastructure (OCI) Cloud Shellは、Linuxシェルへのアクセスを提供するOracle Cloudコンソールからアクセス可能なWebブラウザベースの端末です。SSHキー・ペアをOCI Cloud Shellに作成します。

推定ラボ時間: xx分

### 目標

*   OCI Cloud Shellを使用してSSH鍵ペアを作成します。

### 前提条件

*   OCIコンソールにログインしました。

## タスク1: SSHキー・ペアの作成

1.  クラウド・シェルのオープン ![Cloud Shellを開く](images/sshkeys-01.png)
    
2.  tutorialを実行するように求められたら、Nと入力して入力します。 ![Cloud Shellを開く](images/sshkeys-02.png)
    
3.  コマンドラインで、次をそれぞれ実行してSSKキーを作成します。
    
        <copy>
        mkdir ~/.ssh
        </copy>
        
    
          ```
        cd ~/.ssh \`\`\`
    
        <copy>
        ssh-keygen -b 2048 -t rsa -f my-ssh-key
        </copy>
        
    
    パスフレーズの入力を求められたら、「Enter for no passphrase」をクリックして確認できます。  
    ![キーの作成](images/sshkeys-03.png)
    
4.  コマンドラインで、次を実行して公開キーを表示します。これは後続のステップで使用します。
    
        <copy>
        cat ~/.ssh/my-ssh-key.pub
        </copy>
        
    
    ![公開キーの表示](images/sshkeys-04.png)
    
5.  クラウド・シェルを最小化するには、縮小アイコンをクリックします。
    
    ![クラウド・シェルの縮小](images/sshkeys-05.png)
    
6.  Cloud Shellを再オープンするには、「リストア」ボタンを確認します。後続のステップでCloud Shellを再オープンします。
    
    ![Cloud Shellのリストア](images/sshkeys-06.png)
    

**次の演習に進む**ことができます。

## 謝辞

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **最終更新者/日付** - David Lapp、Database Product Management、2023年6月