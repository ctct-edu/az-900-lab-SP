---
wts:
    title: '11 - CLI を使用して VM を作成する (10 分)'
    module: 'モジュール 03: コア ソリューションおよび管理ツールに関する説明'
---
# 11 - CLI を使用して VM を作成する (10 分)

このチュートリアルでは、Cloud Shell を構成し、Azure CLI を使用してリソース グループと仮想マシンを作成し、Azure Advisor の推奨事項を確認します。 

# タスク 1: Cloud Shell を設定する 

このタスクでは、Cloud Shell を構成してから、Azure CLI を使用して、リソース グループと仮想マシンを作成します。  

1. Azure portal　([https://portal.azure.com](https://portal.azure.com))にサインインします。

2. Azure portal の右上にあるアイコンをクリックして、**Azure Cloud Shell** を開きます。

    ![Azure Portal Azure Cloud Shell アイコンのスクリーンショット。](./images/1002.png)

3. **Bash** と **PowerShell** のどちらかを選択するプロンプトが表示されたら、**Bash**を選択します。 

    **注**：表示されない場合は、CloudShell左上のドロップダウンリストからBashを選択します。

4. **「ストレージがマウントされていません」** と表示された場合、サブスクリプションが「**Azure Pass - スポンサープラン**」となっていることを確認し、「**ストレージの作成**」をクリックします。


# タスク 2: CLI  を使用して、仮想マシンを作成します

このタスクでは、Azure CLI を使用して、リソース グループと仮想マシンを作成します。

1. Cloud Shell 左上のドロップダウン リストで、**「Bash」** が選択されていることを確認します （選択されていない場合は選択して切り替えます）。

    ![「Bash」 ドロップダウンが強調表示された Azure Portal Azure Cloud Shell のスクリーンショット。](./images/1002a.png)


2. 次のコマンドを入力して、リソース グループを確認します。

    ```cli
    az group list --output table
    ```

3. Cloud Shell で以下のコマンドを入力し、最後の行を除くすべての行の最後がバックスラッシュ (`\`) 文字であることを確認します。同じ行にコマンド全体を入力する場合、バックスラッシュ文字は使用しないでください（**##**の部分は自身の受講番号に書き換えて実行）。  

    ```cli
    az vm create \
    --name az900-11-vm1 \
    --resource-group AzureStudent## \
    --image UbuntuLTS \
    --location EastUS \
    --size Standard_DS1_v2 \
    --admin-username student \
    --admin-password Pa55w.rd1234
    ```
    
    > **注**: Windows コンピューターのコマンド ラインを使用している場合は、バックスラッシュ (`\`) 文字をキャレット (`^`) 文字で置き換えます。

    **注**: コマンドの完了には 2 分から 3 分かかります。このコマンドは、仮想マシンと、関連するストレージ、ネットワーク、セキュリティ リソースなどのさまざまなリソースを作成します。仮想マシンのデプロイが完了するまで、次の手順に進まないでください。 

4. コマンドの実行が終了したら、Cloud Shell を閉じます。

5. Azure portal で 「**Virtual Machine**」を検索して選択し、**az900-11-vm1** が実行されていることを確認します。

    ![az900-11-rg1が実行中の状態の仮想マシン ページのスクリーンショット。](./images/1101.png)


# タスク 3: Cloud Shell でコマンドを実行する

このタスクでは、Cloud Shell から CLI コマンドを実行します。 

1. Azure portal の右上にあるアイコンをクリックして、**Azure Cloud Shell** を開きます。

2. Cloud Shell 左上のドロップダウン メニューで、**「Bash」** が選択されていることを確認します。

3. 次のコマンドを実行して、仮想マシンの名前、リソース グループ、場所、状態などの情報を取得します。**PowerState** が「**VM running**」であることを確認してください（**##**の部分は自身の受講番号に書き換えて実行）。 

    ```cli
    az vm show --resource-group AzureStudent## --name az900-11-vm1 --show-details --output table 
    ```

4. 仮想マシンを停止します。仮想マシンの割り当てが解除されるまで請求が続行されることを示すメッセージが表示されます（**##**の部分は自身の受講番号に書き換えて実行）。 

    ```cli
    az vm stop --resource-group AzureStudent## --name az900-11-vm1
    ```

5. 再度、仮想マシンの状態を確認します。**PowerState**が「**VM stopped**」となっていれば、VMが停止していることを確認できました（**##**の部分は自身の受講番号に書き換えて実行）。 

    ```cli
    az vm show --resource-group AzureStudent## --name az900-11-vm1 --show-details --output table 
    ```

# タスク 4: Azure Advisor の推奨事項を確認する

このタスクでは、Azure Advisor の推奨事項を確認します。

   **注:** 前のラボ (「PowerShell を使用して VM を作成する」) を完了している場合、このタスクはすでに実行済みです。 

1. Azure portalで**「アドバイザー」** を検索して選択します。 

2. **「アドバイザー」** ブレードで、**「概要」** を選択します。通知は、信頼性、セキュリティ、パフォーマンス、コスト別にグループ化されて表示されます。 

    ![アドバイザーの概要ページのスクリーンショット。 ](./images/1103.png)

3. 「**推奨**」セクションの**「すべての推奨事項」** を選択し、各推奨事項と推奨されるアクションを表示します。 

    **注:** リソースに応じて、推奨事項は異なります。 

    ![「アドバイザーすべての推奨事項」 ページのスクリーンショット。 ](./images/1104.png)

4. 推奨事項を CSV または PDF ファイルとしてダウンロードできることを確認してください。 

5. アラートを作成できることを確認してください。 

Cloud Shell を構成し、Azure CLI を使用して仮想マシンを作成し、Azure CLI コマンドで練習し、Advisor の推奨事項を確認しました。
