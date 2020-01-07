---
lab:
    title: 'ラボ: Azure にデプロイされた監視サービス'
    module: 'モジュール 5: Azure ソリューションの監視、トラブルシューティング、最適化を行う'
---

# ラボ: Azure にデプロイされた監視サービス
# 受講者ラボ マニュアル

## ラボ シナリオ

素早い市場展開に必要な、次の大きなスタートアップベンチャー向けの API を作成しました。あなたは、迅速に市場に参入したいものの、成長を計画しておらず、リソースが少なすぎたり、ユーザーが多すぎたりして失敗した他のベンチャーを見ています。このために、Microsoft Azure App Service のスケールアウト機能、Application Insights のテレメトリー機能そして Azure DevOps のパフォーマンス テスト機能を活用しようと決めました。この時点で、API Apps を使って API を App Service に展開し、Application Insight を使ってテレメトリーとメトリックスをキャプチャーして、ネットワーク問題や他の過度故障を扱えるスマート クライアントを実装します。Azure DevOps を使うことで、APIのロード テストを行うことになります。

## 目的

このモジュールを修了すると、次のことが可能になります：

-   Application Insights リソースを作成します。

-   Application Insights Telemetry ラッキングを ASP.NET Core Web アプリケーションと Azure Web App リソースと統合する。

-   .NET Foundation ライブラリを使用して、一時的な障害が発生する可能性のあるサービスに対して再試行ポリシーを実装します。

-   Azure DevOps を使用して Web アプリをパフォーマンス テストします。

## ラボのセットアップ

-   **予想時間**：75 分

## 指示

### 開始する前に

#### ラボの仮想マシンへのサインイン

次の認証情報を使用して、**Windows 10** 仮想マシンにサインインしていることを確認します。
    
-   **ユーザー名**： Admin

-   **パスワード**: Pa55w.rd

#### インストールされたアプリケーションの検討

**Windows 10** デスクトップの下部にあるタスク バーを確認します。タスク バーには、このラボで使用するアプリケーションのアイコンが含まれています。
    
-   Microsoft Edge

-   エクスプローラ

-   Visual Studio Code

-   Windows PowerShell

#### 練習用ファイルをダウンロードする

1.  タスク バーで、**Windows PowerShell** アイコンを選択します。

1.  PowerShell コマンド プロンプトで、現在の作業ディレクトリを **Allfiles (F):\\** パスに変更します。

    ```
    cd F:
    ```

1.  コマンド プロンプト内で次のコマンドを入力し、Enter キーを押して、GitHub でホストされている **microsoftlearning/AZ-203-DevelopingSolutionsforMicrosoftAzure** プロジェクトを **Allfiles (F):\\* ドライブにクローンします。

    ```
    git clone --depth 1 --no-checkout https://github.com/microsoftlearning/AZ-203-DevelopingSolutionsForMicrosoftAzure .
    ```

1.  コマンド プロンプト内で次のコマンドを入力し、**Enter** キーを押 して、**AZ-203T05** ラボを完了するために必要なラボ ファイルをチェックアウトします。

    ```
    git checkout master -- Allfiles/*
    ```

1.  現在実行中の **Windows PowerShell** コマンド プロンプト アプリケーションを閉じます。

### エクササイズ 1: Azure リソースの作成と構成

#### タスク 1: Azure portal を開く

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザ ウィンドウで、[**Azure potal**](https://portal.azure.com)(portal.azure.com)に移動します。

1.  サインイン ページで、Microsoft アカウントの **電子メール アドレス**を入力します。

1.  **次へ** を選択します。

1.  Microsoft アカウントの**パスワード**を入力します。

1.  **サインイン** を選択します。

    > **注記**：**Azure potal** に初めてサインインする場合は、ポータルのツアーを提供するダイアログ ボックスが表示されます。ツアーをスキップしてポータルの使用を開始するには、**開始**を選択します。

#### タスク 2: アプリケーション インサイト リソースを作成します。

1.  次の詳細で新規**アプリケーション インサイト アカウント**を作成します:
    
      - **新しいリソースグループ**: MonitoredAssets
    
      - **名前**: instrm\[小文字で名前を指定\]
    
      - **場所**: (US) 米国東部

    > **注記**: Azure が Storage アカウントの作成を完了するのを待ってから、ラボを進みます。アカウントの作成時に通知が届きます。

1.  **アプリケーションインサイト**ブレードの **プロパティ**セクションにアクセス します。

1.  **インストルメンテーション キー**フィールドの値を確認します。このキーは、クライアント アプリケーションによって Application Insights に接続するために使われます。

#### タスク 3: Web アプリ リソースの作成

1.  次の詳細で新規 **Web アプリ**を作成します:

    - **既存のリソース グループ**: MonitoredAssets
    
    - **Web アプリ名**: smpapi\[小文字で名前を指定\]

    - **公開**: コード

    - **ランタイム スタック**: .NET Core 3.0

    - **オペレーティング システム**:Windows

    - **リージョン**: 米国東部

    - **新規App Services  プラン**: MonitoredPlan
    
    - **SKU とサイズ**: Standard (S1)

    - **Application Insights**: 有効

    - **既存の Application Insights リソース**: instrm\[小文字で名前を指定\]

    > **注記**: Azure が Web アプリの作成を完了するのを待ってから、ラボに進みます。アプリの作成時に通知が届きます。

1.  この演習で作成済みの **smpapi\** *Web アプリ*にアクセスします。

1.  ブレードの左側の**設定**セクションで、**構成**セクションに移動します。

1.  [**構成**] セクション内の [**アプリケーション設定**] タブを見つけてアクセスします。

1.  **APPINSIGHTS\_INSTRUMENTATIONKEY** アプリケーション設定キーに対応する値を確認します。この値は、Web アプリ リソースの構築時に自動的に設定されました。

1.  **App Services**ブレードの**プロパティ**セクションにアクセスします。

1.  **URL**フィールドの値を記録します。この値は、ラボの後半で使用され、API に対する要求を行います。

#### タスク 4: Web アプリの自動スケール オプションを構成する

1.  **App Services**ブレードの **スケールアウト**セクションに移動します。

1.  **スケールアウト**セクションで、次の詳細を使用して**カスタム自動スケーリング**を有効にします。
    
    1.  **名前**: ComputeScaler
    
    1.  **スケール モード** セクションで、**メトリックに基づくスケール**を選択します。
    
    1.  **最小インスタンス数**: 2
    
    1.  **最大インスタンス数**: 8
    
    1.  **既定のインスタンス**: 3
    
    1.  **スケールルール**: 既定値を持つ単一スケールアウトルール

1.  変更内容を **自動スケール**構成に**保存**します。

#### 復習

この演習では、このラボの残りの部分で使用するすべてのリソースを作成しました。

### エクササイズ 2: .NET コア Web API アプリケーションのビルド & デプロイ

#### タスク 1: .NET Core Web API プロジェクトの構築

1.  **Visual Studio Code** を起動します。

1.  **Visual Studio Code** で、**Allfiles (F):\\Allfiles\\Labs\\05\\Starter\\Api** フォルダを開きます。

1.  **エクスプローラ**を使用して、コンテキストが現在の作業ディレクトリに設定されている新しいターミナルを開きます。

1.  コマンド プロンプトで、現在のディレクトリに **SimpleApi** という名前の新しい .NET Core Web API アプリケーションを作成します。

    ```
    dotnet new webapi --output . --name SimpleApi
    ```

1.  **2.7.1** バージョンの **Microsoft.ApplicationInsights.AspNetCore** パッケージを NuGet から現在のプロジェクトに追加します。

    ```
    dotnet add package Microsoft.ApplicationInsights.AspNetCore --version 2.7.1
    ```

1.  .NET Core ウェブ アプリケーションの構築

    ```
    dotnet build
    ```

#### タスク 2: HTTPS を無効にして Application Insights を使用するようにアプリケーション コードを更新する

1.  **Visual Studio コード**の**エクスプローラ**を使用 して、エディタで **Startup.cs** ファイルを開きます。

1.  **43**行目で次のコード行を検索して削除します。

    ```
    app.UseHttpsRedirection();
    ```

    > **注記**: このコード行は、Web アプリにHTTPSを強制的に使用します。この演習では不要です。

1.  **Startup** クラス内で、**INSTRUMENTATION_KEY** と名付けられた新しい**静的文字列定数**を、このラボで前に作成した **Application Insights** リソースからコピーした**インストルメンテーション キー**に設定された新しい**静的文字列定数**を追加します。  

    ```
    private static string INSTRUMENTATION_KEY = "{your_instrumentation_key}";
    ```

    > **注記**: たとえば、 **インストルメンテーション キー**が ``d2bb0eed-1342-4394-9b0c-8a56d21aaa43``の場合、コード行は ``private static string INSTRUMENTATION_KEY = "d2bb0eed-1342-4394-9b0c-8a56d21aaa43";`` になります。 

1.  **ConfigureServices** メソッド内に新しいコード行を追加し、提供されたインストルメンテーション キーを使用して Application Insights を構成します。 

    ```
    services.AddApplicationInsightsTelemetry(INSTRUMENTATION_KEY);
    ```

1.  **Startup.cs** ファイルを**保存**します。

1.  **エクスプローラ**を使用して、新しい端末がまだ開いていない場合は、そのコンテキストが現在の作業ディレクトリに設定されます。

1.  .NET Core ウェブ アプリケーションの構築

    ```
    dotnet build
    ```

#### タスク 3: API アプリケーションをローカルでテスト

1.  **エクスプローラ**を使用して、新しい端末がまだ開いていない場合は、コンテキストが現在の作業ディレクトリに設定されている場合に開きます。

1.  .NET Core Web アプリケーションを実行します。

    ```
    dotnet run
    ```

1.  **Microsoft Edge** ブラウザを開きます。

1.  開いているブラウザ ウインドウで、ポート**5000**の **localhost** でホストされているテスト アプリケーションの **/api/values** 相対パスに移動します。
    
    **注記**：完全な URL は<http://localhost:5000/api/values>です。

1.  同じブラウザ ウインドウで、ポート **5000** の **localhost** でホストされているテスト アプリケーションの**/api/values/7**相対パスに移動します。
    
    **注記**：完全な URL は<http://localhost:5000/api/values/7>です。

1.  最近開いたブラウザー ウィンドウを閉じます。

1.  現在実行中の **Visual Studio Code** アプリケーションを閉じます。

#### タスク 4: アプリケーション インサイトでのメトリックの表示

1.  **Azure potal**を表示する、現在開いているブラウザ ウインドウに戻ります。

1.  この実習ラボで前に作成した **instrm\** アプリケーションインサイト アカウントにアクセスします。

1.  **アプリケーション インサイト**ブレードで、ブレードの中央にあるタイルに表示されるメトリックを確認します。具体的には、発生した**サーバー 要求**の数と平均**サーバー応答時間**を確認します。

    > **注記**: 要求が Application Insights のメトリック グラフに表示されるまでに最大 5 分かかる場合があります。

#### タスク 5: Web アプリにアプリケーションをデプロイする

1.  **Visual Studio Code** を起動します。

1.  **Visual Studio Code** で、**Allfiles (F):\\Allfiles\\Labs\\05\\Starter\\Api** フォルダを開きます。

1.  **エクスプローラ**を使用して、コンテキストが現在の作業ディレクトリに設定されている新しいターミナルを開きます。

1.  Microsoft Azure 認証情報を使用して Azure CLIにサインインします。

    ```
    az login
    ```

1.  **MonitoredAssets**リソース グループ内のすべての**アプリ**を一覧表示します。
    
    ```
    az webapp list --resource-group MonitoredAssets
    ```

1.  プレフィックス **smpapi\** を持つ**アプリ**を見つけます。
    
    ```
    az webapp list --resource-group MonitoredAssets --query "[?starts_with(name, 'smpapi')]"
    ```

1.  プレフィックス **smpapi\** を有する単一のアプリの名前のみを印刷します。

    ```
    az webapp list --resource-group MonitoredAssets --query "[?starts_with(name, 'smpapi')].{Name:name}" --output tsv
    ```

1.  現在のディレクトリを、演習ファイルを含む**すべてのファイル (F):\\Allfiles\\Labs\\05\\Starter** ディレクトリに変更します。

    ```
    cd F:\Labfiles\05\Starter\
    ```
1.  この実習ラボで前に作成した **Web アプリ**に **api.zip** ファイルをデプロイします。

    ```
    az webapp deployment source config-zip --resource-group MonitoredAssets --src api.zip --name <name-of-your-api-app>
    ```

    > **注記**: **\<name-of-your-api-app>**を、この実習ラボで前に作成した Web アプリの名前に置き換えます。このアプリ名は、以前のステップで最近クエリしました。

1. この演習で作成済みの **smpapi\** Web アプリにアクセスします。

1. お使いのブラウザで **smpapi\** Web アプリを開きます。

1. ウェブサイトの **/api/values/** 相対パスに対して **GET**要求を実行し、API を使用した結果として返される JSON 配列を観察します。

    > **注記**：たとえば、URL がhttps://smpapistudent.azurewebsites.net の場合、新しい URL はhttps://smpapistudent.azurewebsites.net/api/values となります。

#### 復習

この演習では、ASP.NET Core を使用してAPIを作成し、アプリケーション メトリックをアプリケーション インサイトにストリーミングするように構成しました。次に、Application Insights ダッシュボードを使用して、API のパフォーマンスの詳細を表示しました。

### エクササイズ 3: .NET Core を使ったクライアント アプリケーションの構築

#### タスク 1: .NET Core コンソール プロジェクトの構築

1.  **Visual Studio Code** を起動します。

1.  **Visual Studio Code** で、**Allfiles (F):\\Allfiles\\Labs\\05\\Starter\\Console** フォルダを開きます。

1.  **エクスプローラ**を使用して、コンテキストが現在の作業ディレクトリに設定されている新しいターミナルを開きます。

1.  コマンド プロンプトで、現在のディレクトリに **SimpleConsole** という名前の新しい .NET Core コンソール アプリケーションを作成します。

    ```
    dotnet new console --output . --name SimpleConsole
    ```

1.  NuGetから**Polly**パッケージの **7.1.0** バージョンを現在のプロジェクトに追加します。

    ```
    dotnet add package Polly --version 7.1.0
    ```

1.  .NET Core ウェブ アプリケーションの構築

    ```
    dotnet build
    ```

#### タスク 2: HTTPクライアント コードの追加

1.  **Visual Studio コード**の**エクスプローラ**を使用 して、エディタで**Program.cs** ファイルを開きます。

1.  次の名前空間のファイルの上部に **using** ディレクティブを追加します。
    
      - **System.Net.Http**
    
      - **System.Threading.Tasks**


    ```
    using System.Net.Http;
    using System.Threading.Tasks;
    ```

1.  **7**行目の**プログラム**クラスを見つけます。


    ```
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
    ```

1.  **プログラム**クラス全体を次の実装に置き換えます。


    ```
    class Program
    {
        private const string _api = "";
        private static HttpClient _client = new HttpClient(){ BaseAddress = new Uri(_api) };
    
        static void Main(string[] args)
        {
            Run().Wait();
        }
    
        static async Task Run()
        {
    
        }
    }
    ```

1.  **9** 行目で **\_api** 定数を見つけます:


    ```
    private const string _api = "";
    ```

1.  この演習で前に記録した Web アプリの**URL**に変数の値を設定して、**\_api**定数を更新します。

> **注記**: たとえば、URL がhttp://smpapistudent.azurewebsites.net の場合、新しいコード行は次のようになります: private const string \_api = "http://smpapistudent.azurewebsites.net";

1.  **Run**メソッド内で、次の2行のコードを追加して、**/api/values/** の相対パスに対して文字列を渡す**HttpClient.GetStringAsync** メソッドを非同期的に呼び出し、応答を書き出します。


    ```
    string response = await _client.GetStringAsync("/api/values/");
    Console.WriteLine(response);
    ```

1.  **Program.cs** ファイルを**保存**します。

#### タスク 3: コンソール アプリケーションをローカルでテスト

1.  **エクスプローラ**を使用して、新しい端末がまだ開いていない場合は、コンテキストが現在の作業ディレクトリに設定されている場合に開きます。

1.  .NET Core Web アプリケーションを実行します。

    ```
    dotnet run
    ```

1.  アプリケーションが Azure で Web アプリを正常に呼び出し、この実習で前に説明したのと同じJSONアレイを返すことに注意してください。


    ```
    ["value1","value2"]
    ```

1.  **Azure potal**を表示する、現在開いているブラウザ ウインドウに戻ります。

1.  この演習で作成済みの **smpapi\** Web アプリにアクセスします。

1.  **App Service** ブレードで、**停止**を選択して Web アプリの実行を停止します。

1.  **Visual Studio Code** を起動します。

1.  **Visual Studio Code** で、**Allfiles (F):\\Allfiles\\Labs\\05\\Starter\\Console** フォルダを開きます。

1.  **エクスプローラ**を使用して、コンテキストが現在の作業ディレクトリに設定されている新しいターミナルを開きます。

1. コマンド プロンプトで、.NET Core Web アプリケーションを実行します。


    ```
    dotnet run
    ```

1. アプリケーションが失敗し、次の例外メッセージに似た **HttpRequestException** メッセージが表示されます。


    ```
    System.Net.Http.HttpRequestException: Response status code does not indicate
    success: 403 (Site Disabled).
       at System.Net.Http.HttpResponseMessage.EnsureSuccessStatusCode()
       at System.Net.Http.HttpClient.GetStringAsyncCore(Task`1 getTask)
       at SimpleConsole.Program.Run() in F:\Labfiles\05\Starter\Console\Program.cs:line 20
    ```

    > **注記**: この例外は、Web アプリが使用できなくなったために発生します。

#### タスク 4: Pollyを使用して再試行ロジックを追加する

1.  **Visual Studioコード**の**エクスプローラ**を使用して、エディタで**PollyHandler.cs**ファイルを開きます。

1.  **PollyHandler**クラス内で、**13～24**行目を確認します。これらのコード行は、**NET Foundation** の **Polly** ライブラリを使用して、失敗したHTTP要求を5分ごとに再試行する再試行ポリシーを作成します。

1.  **Visual Studioコード**の**エクスプローラ**を使用 して、エディタで**Program.cs**ファイルを開きます。

1.  **10**行目で**\_client**定数を見つける:


    ```
    private static HttpClient _client = new HttpClient(){ BaseAddress = new Uri(_api) }; 
    ```

1.  **PollyHandler** クラスの新しいインスタンスを使用するように **HttpClient** コンストラクタを更新して **\_client** 定数を更新します。


    ```
    private static HttpClient _client = new HttpClient(new PollyHandler()){ BaseAddress = new Uri(_api) };
    ```

1.  **Program.cs** ファイルを**保存**します。

#### タスク 5: 再試行ロジックを検証する

1.  **エクスプローラ**を使用して、新しい端末がまだ開いていない場合は、コンテキストが現在の作業ディレクトリに設定されている場合に開きます。

1.  .NET Core Web アプリケーションを実行します。


    ```
    dotnet run
    ```

1.  HTTP要求の実行は引き続き失敗し、5秒ごとに再試行されている事を確認してください。アプリケーションを実行したままにします。成功するまで、Web アプリに無限にアクセスしようとします。

1.  **Azure potal**を表示する、現在開いているブラウザ ウインドウに戻ります。

1.  この演習で作成済みの **smpapi\** Web アプリにアクセスします。

1.  **App Service** ブレードで、**開始**を選択して Web アプリを再開します。

1.  現在実行中の **Visual Studio Code** アプリケーションに戻ります。

1.  アプリケーションが最終的に Azure で Web アプリを正常に呼び出し、この実習で前に説明したのと同じ JSON アレイを返すことに注意してください。

1.  現在実行中の **Visual Studio Code** アプリケーションを閉じます。

#### 復習 

この演習では、条件付き再試行ロジックを使用してAPIにアクセスするコンソール アプリケーションを作成しました。API が利用可能かどうかにかかわらず、アプリケーションは引き続き動作します。

### エクササイズ 4: テスト Web アプリの読み込み

#### タスク 1: Web アプリでパフォーマンス テストを実行する

1.  **Azure potal**を表示する、現在開いているブラウザ ウインドウに戻ります。

1.  この演習で作成済みの **smpapi\** Web アプリにアクセスします。

1.  **App Services** ブレードで、**パフォーマンス テスト**リンクを選択します。

1.  次の詳細を使用して、新しい **パフォーマンス テスト** を作成します。
    
      - **名前**: LoadTest
    
      - **以下から負荷を生成**: 米国東部 (Web アプリの場所)
    
      - **ユーザーの読み込み**: 1000
    
      - **時間**: 10
    
      - **テスト タイプ**: 手動テスト
    
      - **URL**: http://\<your-api-name\>.azurewebsites.net/api/values

1.  **LoadTest**ブレードで、テストが開始され、完了するのを待ってから、演習に進みます。Web アプリの使用率が増加するにつれて、ライブ チャートが更新します。

    > **注記**: ほとんどのロード テストでは、リソースの収集と開始に約10～15分かかります。ロード テストが開始されると自動的にリフレッシュするので、このブレードで待てます。ロード テストには、この演習の前の手順で指定した10分かかります。

#### タスク 2: パフォーマンス テスト後に Azure モニタのメトリックを使用する

1.  **Azure モニタ**サービスに移動します。

1.  **モニタ** ブレードで、**メトリック**リンクを選択します。

1.  **メトリック**セクションで、次の詳細を含む新しいグラフを作成します。
    
      - **リソース**: この実習ラボで前に作成した instrm\* Application Insights アカウント
    
      - **時間範囲**: 最後の30分 (自動)
    
      - **グラフの種類**: 面グラフ

1.  次の詳細情報を使用して新規メトリックを作成:
    
      - **メトリック名前空間**: 標準メトリック
    
      - **メトリック**: プロセス CPU
    
      - **集計**: 平均

1.  次の詳細情報を使用して別の新規メトリックを作成:
    
      - **メトリック名前空間**: ログベースのメトリック
    
      - **メトリック**: サーバーの応答時間
    
      - **集計**: 平均

1.  グラフに表示される情報を確認してください。アプリケーションの負荷が増大するにつれて、サーバーの応答時間と CPU 時間とどのように相関するかを確認してください。

#### 復習

この演習では、Azure で使用できるツールを使用して、Web アプリのパフォーマンス（読み込み）テストを実行しました。ロード テストを実行した後、Azure Monitor インターフェイスでメトリックを使用してAPI アプリの動作を測定できます。

### エクササイズ 5: サブスクリプションのクリーンアップ 

#### タスク 1: Cloud Shell を開く

1.  Azure potalの上部で、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。

1.  **クラウドシェル**がまだ構成されていない場合は、既定の設定を使用して Bash のシェルを構成します。

1.  **Cloud Shell** コマンド プロンプトのポータルの下部にある次のコマンドを入力し、Enter キーを押してサブスクリプション内のすべてのリソース グループを一覧表示します。


    ```
    az group list
    ```

1.  次のコマンドを入力し、Enter キーを押して、リソース グループを削除する可能性のあるコマンドの一覧を表示します。


    ```
    az group delete --help
    ```

#### タスク 2: リソース グループを削除する

1.  次のコマンドを入力し、Enter キーを押して **MonitoredAssets** リソース グループを削除します。


    ```
    az group delete --name MonitoredAssets --no-wait --yes
    ```
    
1.  ポータルの下部にある **Cloud Shell** ペインを閉じます。

#### タスク 3: アクティブなアプリケーションを閉じる

1.  現在実行中の **Microsoft Edge** アプリケーションを閉じます。

1.  現在実行中の **Visual Studio Code** アプリケーションを閉じます。

#### 復習

この実習では、この演習で使用する **リソース グループ** を削除してサブスクリプションをクリーンアップしました。
