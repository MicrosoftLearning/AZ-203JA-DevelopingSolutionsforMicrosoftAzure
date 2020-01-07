---
lab:
    title: 'ラボ: イメージとコンテナを使用してコンピューティング ワークロードをデプロイする'
    module: 'モジュール 1: サービスとしての Azure インフラストラクチャの開発 (IaaS) コンピューティング ソリューション'
---

# ラボ: イメージとコンテナを使用してコンピューティング ワークロードをデプロイする
# 受講ラボマニュアル

## ラボ シナリオ

あなたの組織では、タスクを実行して直ちに終了する仮想マシン (VM) を自動的に作成する方法を模索しています。Microsoft Azure で複数のコンピューティング サービスを評価し、仮想化されたマシンを自動的に作成し、それらのコンピューターにカスタム ソフトウェアをインストールするのに役立つサービスを決定する必要があります。概念実証として、2 つのソリューションを比較できるように、VHD イメージとコンテナー イメージから VM を作成することにしました。概念実証を簡潔に保つには、.NET Core で書かれた特別な "IP チェック" アプリケーションを作成し、マシンに自動的にデプロイします。概念実証では、 Azure Container Instances と Azure 仮想マシン サービスを評価します。

## 目的

このモジュールを修了すると、次のことが可能になります：

-   Azure potal のツールを使用して VM を作成する。

-   Docker コンテナー イメージを Azure Container Registry にデプロイする。

-   Azure Container Instances を使用して、Azure Container Registry のコンテナー イメージからコンテナーをデプロイする。

-   Azure Resource Manager テンプレートと Azure Container Registry のコンテナー イメージを使用して VM をデプロイする。

## ラボのセットアップ

-   **予想時間**：75 分

## 指示

### 開始する前に

#### ラボの仮想マシンへのサインイン

次の認証情報を使用して、**Windows 10** 仮想マシンにサインインしていることを確認します。
    
- **ユーザー名**：Admin
    
- **パスワード**: Pa55w.rd

#### インストールされたアプリケーションの検討

**Windows 10** デスクトップの下部にあるタスク バーを確認します。タスク バーには、このラボで使用するアプリケーションのアイコンが含まれています。
    
-   Microsoft Edge
    
-   エクスプローラ

### エクササイズ 1: Azure potal を使用した仮想マシンの作成

#### タスク 1: Azure potalを開く

1.  **Azure potal**(<https://portal.azure.com>) にサインインします。

2.  Azure potal に初めてサインインする場合は、ダイアログ ボックスが表示され、ポータルのツアーが開始されます。ツアーをスキップするには、**開始** を選択します。

#### タスク 2: リソース グループの作成

1.  次の詳細で新規 **リソース グループ** を作成します:
    
    1.  **名前**: ContainerCompute
    
    2.  **場所**：米国東部

2.  演習を進める前に、作成タスクが完了するまで待ちます。

#### タスク 3: Linux 仮想マシンリソースの作成

1.  次の詳細で新規 **仮想マシン** を作成します:
    
      - **オペレーティング·システム**: Ubuntu サーバー 18.04 LTS
    
      - **名前**: simplevm
    
      - **ディスクタイプ**：SSD
    
      - **ユーザー名**：受講者
    
      - **パスワード**: StudentPa55w.rd
    
      - **リソースグループ**: ContainerCompute
    
      - **場所**：米国東部
    
      - **サイズ**: StandardB1s
    
      - **パブリック インバウンド ポート**: SSH (22)

2.  この演習を続行する前に、作成タスクが完了するのを待ちます。

#### タスク 4: 仮想マシンのバックアップ

1.  この演習で作成済みの **simplevm** VM にアクセスします。

2.  **仮想マシンへの接続** ポップアップを開きます。 

3.  ポート**22** と **パブリック IP アドレス** を使用して VM に接続するには、**SSH コマンド** をコピーします。      このコマンドは、この実習の後半で使用します。

4.  Azure potalで新しい **Cloud Shell** インスタンスを開きます。 

5.  **クラウドシェル** がまだ構成されていない場合は、既定の設定を使用して Bash のシェルを構成します。 

6.  **クラウドシェル** コマンド プロンプト内で、この演習で前にコピーした **SSH コマンド** を使用して、SSH を使用してVMに接続します。   

7.  接続プロセス中に、ホストの信頼性を確認できないという警告が表示されます。ホストへの接続を続行します。最後に、資格情報の入力を求められたときに、**PasswordPa55w.rd** を使用します。

8.  VM に接続している場合は、次のコマンドを使用してマシンに関する情報を表示します。

    ```
    uname -mnipo
    ```
    ```
    uname -srv
    ```

9.  **Cloud Shell** ペインを閉じます。 

#### 復習

この演習では、Azure potal インターフェイスを使用して新しい VM を手動で作成し、Cloud Shell と セキュアシェル （SSH）を使用して VM に接続しました。

### エクササイズ 2: Azure CLI を使用して Linux 仮想マシンを作成する 

#### タスク 1: Cloud Shell を開く

1.  Azure potalで新しい **Cloud Shell** インスタンスを開きます。

#### タスク 2: Azure CLI を使用して、次のように入力します。

1.  **az** コマンドを **--help** フラグと共に使用して、CLIのルート・レベルにあるサブグループおよびコマンドのリストを表示します。   

2.  **az vm** コマンドを **--help** フラグと共に使用して、**仮想マシン** のサブグループとコマンドのリストを表示します。     

3.  **az vm create** コマンドを  **--help** フラグで使用して、**仮想マシンの作成** コマンドの引数と例のリストを表示します。     

4.  **az vm create** コマンドを使用して、次の設定で新しい **仮想マシン** を作成します。 
    
      - **リソースグループ**: ContainerCompute
    
      - **名前**: quickvm
    
      - **画像**: Debian
    
      - **ユーザー名**：受講者
    
      - **パスワード**: StudentPa55w.rd

5.  VM 作成のプロセスが完了するまで待ちます。プロセスが完了すると、コマンドはマシンに関する詳細を含む JSON ファイルを返します。

6.  **az vm show** コマンドを使用して、新しく作成されたVMに関するさまざまなメタデータを含む、より詳細な JSON ファイルを表示します。 

7.  **az vm list-ip-addresses** コマンドを使用して、VM に関連付けられているすべての IP アドレスを一覧表示します。 

    ```
    az vm list-ip-addresses --resource-group ContainerCompute --name quickvm
    ```

8.  **az vm list-ip-address** コマンドと **--query** 引数を使用して、出力をフィルター処理して最初のIPアドレス値のみを返します。   

    ```
    az vm list-ip-addresses --resource-group ContainerCompute --name quickvm --query '[].{ip:virtualMachine.network.publicIpAddresses[0].ipAddress}' --output tsv
    ```

9.  前のコマンドの結果を *ipAddress* という名前の新しいBashシェル変数に格納するには、次のスクリプトを使用 します。 

    ```
    ipAddress=$(az vm list-ip-addresses --resource-group ContainerCompute --name quickvm --query '[].{ip:virtualMachine.network.publicIpAddresses[0].ipAddress}' --output tsv)
    ```

10. Bash シェル変数 *ipAddress* の値を印刷するには、次のスクリプトを使用します。

    ```
    echo $ipAddress
    ```

11. 次のスクリプトを使用して、SSH ツールと Bash シェル変数 *ipAdwdress* に格納されている IP アドレスを使用して、この演習で前に作成したVMに接続します。

    ```
    ssh student@$ipAddress
    ```

12. 接続プロセス中に、ホストの信頼性を確認できないという警告が表示されます。ホストへの接続を続行します。最後に、資格情報の入力を求められたときに、**StudentPa55w.rd** を使用します。

13. VM に接続したら、次のコマンドを使用してマシンに関する情報を監視し、正しい VM に接続していることを確認します。

    ```
    uname -mnipo
    ```
    ```
    uname -srv
    ```

14. **Cloud Shell** ペインを閉じます。

#### 復習

この演習では、Azure Cloud Shell を使用して、自動化されたスクリプトの一部として仮想マシンを作成しました。

### エクササイズ 3: Docker コンテナー イメージを作成し、Azure Container Registry にデプロイする

#### タスク 1: Cloud Shell とエディタを開く

1.  Azure potalで新しい **Cloud Shell** インスタンスを開きます。

2.  **Cloud Shell** コマンド プロンプトで、アクティブ ディレクトリを **\~/clouddrive** に変更します。 

    > **注記**：Bashのディレクトリを変更するコマンドは **cd \<パス\>** です。 

3.  Cloud Shell コマンド プロンプトで、**\~/clouddrive** ディレクトリ内に **ipcheck** という名前の新しいディレクトリを作成します。   

    > **注記**：Linuxで新しいディレクトリを作成するコマンドは **mkdir \<ディレクトリ名\>** です。 

4.  アクティブ ディレクトリを **\~/clouddrive/ipcheck** に変更します。 

5.  **dotnet new console --output .** を使用します。 **--name ipcheck** コマンドを使用して、現在のディレクトリに新しい .NET Core コンソール アプリケーションを作成します。

6.  **Dockerfile** という名前の **\~/clouddrive/ipcheck** ディレクトリに新しいファイルを作成します。   

    > **注記**：Bashで新しいファイルを作成するコマンドは、**touch \<ファイル名\>** です。  ファイル名 **Dockerfile** は大文字と小文字を区別します。 

7.  現在のディレクトリのコンテキストで埋め込みグラフィカルエディタを開きます。

    > **注記**：エディタを開くには、**code .** コマンドを使用するか、エディタ ボタンを選択します。 

#### タスク 2: .NET Core アプリケーションの作成とテスト

1.  グラフィカル エディタで、**Program.cs** ファイルを開き、その内容を次のコードに置き換えてから、ファイルを保存します。 

    ```
    public class Program
    {
        public static void Main(string[] args)
        {        
            if (System.Net.NetworkInformation.NetworkInterface.GetIsNetworkAvailable())
            {
                System.Console.WriteLine("Current IP Addresses:");
                string hostname = System.Net.Dns.GetHostName();
                System.Net.IPHostEntry host = System.Net.Dns.GetHostEntry(hostname);
                foreach(System.Net.IPAddress address in host.AddressList)
                {
                    System.Console.WriteLine($"\t{address}");
                }
            }
            else
            {
                System.Console.WriteLine("No Network Connection");
            }
        }
    }
    ```

2.  コマンド プロンプトの **dotnet run** コマンドを使用してアプリケーションを実行し、1つ以上のIPアドレスが見つかったことを検証します。 

3.  グラフィカル エディタで **Dockerfile** ファイルを開き、その内容を次のコードに置き換えてから、ファイルを **保存** します。  

    ```
    FROM mcr.microsoft.com/dotnet/core/sdk:2.2-alpine AS build
    WORKDIR /app

    COPY *.csproj ./
    RUN dotnet restore

    COPY . ./
    RUN dotnet publish --configuration Release --output out

    FROM mcr.microsoft.com/dotnet/core/runtime:2.2-alpine
    WORKDIR /app

    COPY --from=build /app/out .

    ENTRYPOINT ["dotnet", "ipcheck.dll"]
    ```

4.  **Cloud Shell** ペインを閉じます。

#### タスク 3: Azure Container Registry リソースの作成

1.  次の詳細で新規 **コンテナ登録** を作成します:
    
      - **名前**: \<Any globally unique name\>
    
      - **リソースグループ**: ContainerCompute
    
      - **場所**：米国東部
    
      - **管理者ユーザー**: 無効にする
    
      - **スク**: Basic

2.  この演習を続行する前に、作成タスクが完了するのを待ちます。

#### タスク 4: Cloud Shell を開き、Azure Container Registry メタデータを格納する

1.  新しい **Cloud Shell** インスタンスを開 きます。

2.  **Cloud Shell** コマンド プロンプト内で、**az acr list** コマンドを使用して、サブスクリプション内のすべての **Container Registry** の一覧を表示します。   

3.  最後に作成した **Container Registry** の名前を出力するには、次のコマンドを使用します。

    ```
    az acr list --query "max_by([], &creationDate).name" --output tsv
    ```

4.  Bash シェル変数 *acrName*に最後に作成した **Container Registry** の名前を保存するには、次のコマンドを使用します。

    ```
    acrName=$(az acr list --query "max_by([], &creationDate).name" --output tsv)
    ```

5.  Bash シェル変数 *acrName* の値を印刷するには、次のスクリプトを使用します。

    ```
    echo $acrName
    ```

#### タスク 5: Docker CLIコンテナー イメージを Azure Container Registry にデプロイする

1.  アクティブ ディレクトリを **\~/clouddrive/ipcheck** に変更します。

2.  **dir** コマンドを使用して、現在のディレクトリの内容を表示します。 

    > **注記**： この実習ラボで前に編集し た **Program.cs** ファイルと **Dockerfile** ファイルの両方が存在する場合は、正しいディレクトリにいることがわかります。

3.  次のコマンドを使用して、ソース コード- **Container Registry** にアップロードし、コンテナー イメージ を **Azure Container Registry タスク** としてビルドします。 

    ```
    az acr build --registry $acrName --image ipcheck:latest .
    ```

4.  この演習を進める前に、ビルド タスクが完了するのを待ちます。

5.  **Cloud Shell** ペインを閉じます。

#### タスク 6: Azure Container Registry でコンテナー イメージを検証する

1.  この実習ラボで前述したContainer Registry にアクセスします。

2.  レジストリに保存されているイメージを表示するには、**リポジトリ** リンクを選択します。

3.  **画像** ブレードと **タグ** ブレードを使用して、**ipcheck** イメージに関連付けられたメタデータを **最新の** タグで表示します。   

    > **注記**：ID の実行 ハイパーリンクを選択して、ビルド タスクメタデータを表示することもできます。

#### 復習

この演習では、マシンの現在の IP アドレスを表示する .NET Core コンソール アプリケーションを作成しました。次に Dockerfile ファイルをアプリケーションに追加して、Docker コンテナー イメージに変換できるようにしました。最後に、コンテナー イメージを Azure  Container Registry にデプロイしました。

### エクササイズ 4: Azure コンテナ- インスタンスをデプロイする 

#### タスク 1: Azure Container Registry で管理者ユーザーを有効にする

1.  この実習ラボで前述したContainer Registry にアクセスします。

2.  Container Registry の設定を表示するには、**更新** ボタンを選択します。

3.  **管理者ユーザー** を **有効にします**。

    > **注記**: 変更内容は自動的に保存されます。

#### タスク 2: コンテナー イメージを Azure  コンテナ- インスタンスに自動的にデプロイする

1.  レジストリに保存されているイメージを表示するには、**リポジトリ** リンクを選択します。

2.  **ipcheck** イメージを選択し、そのイメージの **最新の** タグを表示します。 

3.  **ipcheck** コンテナー イメージの **最新の** タグを選択/右クリックして、  次の設定で  新しい **Azure コンテナ- インスタンス** をデプロイします。
    
      - **コンテナ名**: managedcompute
    
      - **OS タイプ**: Linux
    
      - **リソースグループ**: ContainerCompute
    
      - **場所**：米国東部
    
      - **コア数**: 2
    
      - **メモリ (GB)**: 4
    
      - **パブリック IP アドレス**: いいえ

4.  この演習を続行する前に、作成タスクが完了するのを待ちます。

#### タスク 3: コンテナー イメージを Azure コンテナ- インスタンスに手動でデプロイする

1.  この実習ラボで前述したContainer Registry にアクセスします。

2.  別の サービスからContainer Registry にアクセスするために必要な認証情報を表示するには、**アクセス キー** リンクを選択します。このセクションの次の値を記録して、この演習の後半で使用します。
    
      - **ログイン サーバー**
    
      - **ユーザー名**
    
      - **パスワード**

    > **注記**：これらの値は、別のコンテナ- インスタンスを作成するときに、この演習の後半で使用します。

3.  この実習ラボで前に記録した**アクセスキー**の資格情報を使用して、次の詳細を含む新しい **コンテナ- インスタンス** を作成します。
    
      - **コンテナ名**: manualcompute
    
      - **コンテナイメージの種類**: プライベート
    
      - **コンテナイメージ**: \<Login server recorded earlier in the lab \>/ipcheck:latest
    
      - **画像レジストリログインサーバー**: \<Login server recorded earlier in the lab\>
    
      - **イメージ レジストリのユーザー名**: \<Username recorded earlier in the lab \>
    
      - **画像レジストリパスワード**: \<Password recorded earlier in the lab \>
    
      - **リソースグループ**: ContainerCompute
    
      - **場所**：米国東部
    
      - **OSタイプ**: Linux
    
      - **コア数**: 1
    
      - **メモリ (GB)**: 1.5
    
      - **パブリック IP アドレス**: はい
    
      - **ポート**: 80
    
      - **追加のアニメーションを開く**: いいえ
    
      - **ポート プロトコル**: TCP
    
      - **ポリシーの再起動**: 失敗時

4.  演習を進める前に、作成タスクが完了するまで待ちます。

#### タスク 4: コンテナ- インスタンスが正常に実行されたことを検証する

1.  この実習ラボで前述した **手動計算** Container Registry にアクセスします。

2.  **コンテナ** リンクを選択すると、実行中の現在のコンテナの一覧が表示されます。 

3.  **ipcheck** アプリケーションを実行したコンテナ- インスタンスの **イベント** リストの内容を表示します。

4.  [**ログ**] タブを選択し、コンテナー インスタンスのテキスト ログを確認します。 

> **注記**: 必要に応じて、**managedcompute** コンテナー インスタンスから**イベント**と**ログ**を表示することもできます。

#### 復習

この演習では、複数のメソッドを使用して、コンテナー イメージを Azure コンテナ- インスタンスにデプロイしました。手動メソッドを使用すると、デプロイをさらにカスタマイズし、コンテナの実行の一部としてタスク ベースのアプリケーションを実行することもできます。

### エクササイズ 5: サブスクリプションのクリーンアップ 

#### タスク 1: Cloud Shell を開き、リソース グループを一覧表示する

1.  Azure potalの上部で、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。 

2.  ポータルの下部にある **Cloud Shell** コマンド プロンプトで次のコマンドを入力し、Enter キーを押してサブスクリプション内のすべてのリソース グループを一覧表示します。

    ```
    az group list
    ```

3.  次のコマンドを入力し、Enter キーを押して、リソース グループを削除する可能性のあるコマンドの一覧を表示します。

    ```
    az group delete --help
    ```

#### タスク 2: リソース グループを削除する

1.  次のコマンドを入力し、Enter キーを押して **ContainerCompute** リソース グループを削除します。

    ```
    az group delete --name ContainerCompute --no-wait --yes
    ```

2.  ポータルの下部にある **Cloud Shell** ペインを閉じます。 

#### タスク 3: アクティブなアプリケーションを閉じる

1.  現在実行中の **Microsoft Edge** アプリケーションを閉じます。

#### 復習

この実習では、この演習で使用する **リソース グループ** を削除してサブスクリプションをクリーンアップしました。
