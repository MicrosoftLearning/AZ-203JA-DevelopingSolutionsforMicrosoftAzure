---
lab:
    title: 'ラボ: ポリグロットデータソリューションの構築'
    type: 'Answer Key'
    module: 'モジュール 3：Azure storage 向けの開発'
---

# ラボ: ポリグロット データ ソリューションの構築
# 受講ラボの解答キー

## Microsoft Azure ユーザー インターフェイス

Microsoft クラウド ツールのダイナミックな性質を考えると、このトレーニング コンテンツの開発後に Azure ユーザー インターフェイス (UI) の変更が発生する可能性があります。これらの変更により、演習の指示と手順が正しく一致しない場合があります。

Microsoft は、コミュニティが必要な変更を行うとすぐに、このトレーニング コースを更新します。しかし、クラウド更新が頻繁に起きるため、この研修内容が更新される前に、UI の変更を経験するかも知れません。**その場合は変更に順応して、必要に応じてラボでをそれを処理してください。**

## 指示

### 開始する前に

#### ラボの仮想マシンへのサインイン

  - 次の認証情報を使用して **Windows 10** 仮想マシンにサインインします。
    
      - **ユーザー名**： Admin
    
      - **パスワード**: Pa55w.rd

> > **注記**： ラボ仮想マシンのサインイン手順は、インストラクターから提供されます。

#### インストールされたアプリケーションの検討

  - **Windows 10** デスクトップの下部にあるタスク バーを確認します。タスク バーには、このラボで使用するアプリケーションのアイコンが含まれています。
    
      - Microsoft Edge
    
      - エクスプローラ
    
      - Visual Studio Code:

#### 練習用ファイルをダウンロードする

1.  タスク バーで、**Windows PowerShell** アイコンを選択します。

2.  PowerShell コマンド プロンプトで、現在の作業ディレクトリを **Allfiles (F):\\** パスに変更します。

    ```
    cd F:
    ```

3.  コマンド プロンプト内で次のコマンドを入力し、Enter キーを押して、GitHub でホストされている **Microsoftlearning/AZ-203-DevelopingSolutionsForAzure** プロジェクトを **Labfiles** ディレクトリに複製します。

    ```
    git clone --depth 1 --no-checkout https://github.com/microsoftlearning/AZ-203-DevelopingSolutionsForMicrosoftAzure .
    ```

4.  コマンド プロンプト内で次のコマンドを入力し、**Enter**  キーを押 して、**AZ-203.02** ラボを完了するために必要なラボ ファイルをチェックアウトします。

    ```
    git checkout master -- Allfiles/*
    ```

5.  現在実行中の **Windows PowerShell** コマンド プロンプト アプリケーションを閉じます。

### エクササイズ 1: Azure 内にデータベース リソースを作成

#### タスク 1: Azure portalを開く

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

2.  開いているブラウザ ウインドウで、**Azure portal** ([portal.azure.com](https://portal.azure.com))に移動します。

3.  Microsoft アカウントの **電子メール アドレス** を入力します。

4.  **次へ** を選択します。

5.  Microsoft アカウントの **パスワード** を入力します。 

6.  **サインイン** を選択します。

> > 注記： **Azure portal** に初めてサインインする場合は、ポータルのツアーを提供するダイアログ ボックスが表示されます。  ツアーをスキップしてポータルの使用を開始するには、**開始** を選択します。

#### タスク 2: SQLデータベースリソースを作成する

1.  Azureポータルの左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーションペインをクリックしてください。

2.  **すべてのサービス** ブレードで、**SQLサーバー** を選択します。

3.  **SQLサーバー** ブレードで、SQL サーバー インスタンスの一覧を表示します。 

4.  **SQLサーバー** ブレードの上部にある **追加** を選択します。

5.  **SQLサーバー（論理サーバーのみ）** ブレードで、次の操作を実行します。
    
    1.  **サーバー名** フィールドに、値 **polysqlsrvr\[名前を小文字で入力\]** と入力します。
    
    2.  **サーバー管理者ログイン** フィールドに、値 **testuser** を入力します。 
    
    3.  **パスワード** フィールドに、値 **TestPa$$w0rd**. を入力します。
    
    4.  **パスワードの確認** フィールドに、値 **TestPa$$w0rd** をもう一度入力します。  
    
    5.  **サブスクリプション** ドロップダウン リストは既定値に設定したままにします。 
    
    6.  **リソース グループ** セクションで、**新規作成** を選択し、**PolyglotData** を入力し、**OK** を選択します。
    
    7.  **場所** ドロップダウン リストで、**米国東部** オプションを選択します。
    
    8.  **Azure Services にサーバーへのアクセスを許可する** セクションで、チェックボックスがオンであることを確認します。 
    
    9.  **高度なデータ セキュリティ** セクションで、**今すぐ表示しない** オプションを選択します。   
    
    10. **作成** を選択します。

6.  演習を進める前に、作成タスクが完了するまで待ちます。

7.  Azureポータルの左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーションペインをクリックしてください。

8.  **すべてのサービス** ブレードで、**SQL データベース** を選択します。

9.  **SQL データベース** ブレードで、SQL データベース インスタンスの一覧を表示します。 

10. **SQL データベース** ブレードの上部にある **追加** を選択します。

11. **SQL データベースの作成** ブレードで、**基本**、**追加設定** および **タグ** などのタブをブレードの上部にあるタブに従います。 

> 注記：各タブは、新しい **Azure SQL データベース**.を作成するためのワークフローのステップを表します。 いつでも **レビュー + 作成** を選択して、残りのタブをスキップできます。 

12. **基本** タブで、次の操作を実行します：
    
    11. **サブスクリプション** テキスト ボックスは既定値のままにします。 
    
    12. **リソース グループ** セクションで、リストから **ポリグロットデータ** を選択します。   
    
    13. **データベース** **名** テキスト ボックスに、**polysqldb** を入力します。   
    
    14. **サーバー** フィールドで、**polysqlsrvr\[小文字で名前を入力\** オプションを選択します。 
    
    15. **SQL エラスティック プールを使用する** セクションで、**いいえ** オプションを選択します。   
    
    16. **計算 + ストレージ** オプションを既定値に設定したままにします。 
    
    17. **レビュー + 作成** を選択します。 

13. **レビュー + 作成** タブで、前の手順で選択したオプションを確認します。 

14. 指定した構成を使用してストレージ アカウントを作成するには、**作成** を選択します。

15. 演習を進める前に、作成タスクが完了するまで待ちます。

16. Azureポータルの左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーションペインをクリックしてください。

17. **すべてのサービス** ブレードで、**SQL データベース** を選択します。

18. **SQL データベース** ブレードで、**polysqldb** という名前の SQL データベース インスタンスを選択します。   

19. **SQL データベース** ブレードで、 ブレードの左側にある **設定** セクションを見つけ、**接続文字列** リンクを選択します。     

20. **接続文字列** ペインで、**ADO.NET** 接続文字列の値をコピーします。 *{your\_username} *と *{\_password} *のプレースホルダ値を、 それぞれtestuser****およびTestPa$$w0 rdの値に置き換えて下さい。

> > 注記：たとえば、コピーした接続文字列が

    Server=tcp:polysqlsrvrstudent.database.windows.net,1433;Initial Catalog=polysqldb;Persist Security Info=False;User ID={your_username};Password={your_password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;,

> > 更新された文字列は以下のようになります

    Server=tcp:polysqlsrvrstudent.database.windows.net,1433;Initial Catalog=polysqldb;Persist Security Info=False;User ID=testuser;Password=TestPa$$w0rd;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

21. Azureポータルの左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーションペインをクリックしてください。

22. **すべてのサービス** ブレードで、**SQLサーバー** を選択します。

23. **SQLサーバー** ブレードで、プレフィックス **polysqlsrvr** を持つ SQL サーバー インスタンスを選択します。 

24. **SQL Server** ブレードで、ブレードの 左側にある **セキュリティ** セクションを見つけ、**ファイアウォールと仮想ネットワーク** リンクを選択します。   

25. **ファイアウォールと仮想ネットワーク** ペインで、**クライアント IP を追加** を選択して、許可されている IP アドレス範囲の一覧に仮想マシンの IP アドレスを追加します。   

26. ブレードの上部にある **保存** をクリックします。

> > 注記：ファイアウォールの変更がサーバー上で更新されるまで数分かかる場合があります。

27. 保存操作が完了したら、**OK** を選択して確認ダイアログを閉じます。 

#### タスク 3: Azure Cosmos DB アカウント リソースの作成

1.  Azureポータルの左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーションペインをクリックしてください。

2.  **すべてのサービス** ブレードで、**Azure コスモス DB** を選択します。

3.  **Azure コスモス DB** ブレードで、Azure Cosmos DB インスタンスの一覧を表示します。 

4.  **Azure Cosmos DB** ブレードの上部にある **追加** を選択します。

5.  **Azure Cosmos DB アカウントの作成** ブレードで、**基本**、**ネットワーク** および **タグ** などのブレードの上部にあるタブを確認します。

> 注記：各タブは、新しい **Azure Cosmos DB アカウントを作成** するためのワークフローのステップを表します。いつでも **レビュー + 作成** を選択して、残りのタブをスキップできます。

6.  **基本** タブで、次の操作を実行します：
    
    1.  **サブスクリプション** テキスト ボックスは既定値のままにします。 
    
    2.  **リソース グループ** セクションで、リストから **ポリグロットデータ** を選択します。
    
    3.  **アカウント** **名** テキスト ボックスに、 **polycosmos\[名前を小文字で\]** 入力します。.    
    
    4.  API **** ドロップダウン リストで、**コア (SQL)** オプションを選択します。   
    
    5.  **場所** ドロップダウン リストで、 **米国東部** リージョンを選択します。 
    
    6.  **地理冗長性** セクションで、**無効にする** オプションを選択します。
    
    7.  **マルチリージョン書き込み** セクションで、**無効** オプションを選択します。   
    
    8.  **レビュー + 作成** を選択します。

7.  **レビュー + 作成** タブで、前の手順で選択したオプションを確認します。

8.  指定した構成を使用してストレージ アカウントを作成するには、**作成** を選択します。

9.  演習を進める前に、作成タスクが完了するまで待ちます。

10. Azureポータルの左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーションペインをクリックしてください。

11. **すべてのサービス** ブレードで、**Azure コスモス DB** を選択します。

12. **Azure Cosmos DB** ブレードで、プレフィックス **polycosmos** を含む Azure Cosmos DB アカウント インスタンスを選択します。 

13. **Azure Cosmos DB アカウント** ブレードで、 ブレードの左側にある **設定** セクションを見つけて、**キー** リンクを選択します。

14. **キー** ペインで、**URI** フィールドと **プライマリーキー** フィールドの値を記録します。 これらの値は、この演習の後半で使用します。

#### タスク 4: Azure Storage  アカウント リソースの作成

1.  Azureポータルの左側にあるナビゲーションペインで、**すべてのサービス**ナビゲーションペインをクリックしてください。

2.  **すべてのサービス** ブレードで、**ストレージ アカウント** を選択します。

3.  **ストレージ アカウント** ブレードで、ストレージ インスタンスの一覧を表示します。 

4.  **ストレージ アカウント** ブレードの上部にある **追加** を選択します。

5.  **ストレージ アカウントを作成** ブレード で、**基本**、**詳細** および **タグ** などのブレードの上部にあるタブを確認します。

> 注記：各タブは、ワークフロー内の新しい **Azure Storage アカウント** を作成するためのステップを表します。いつでも **レビュー + 作成** を選択して、残りのタブをスキップできます。

6.  **基本** タブで、次の操作を実行します：
    
    1.  **サブスクリプション** テキスト ボックスは既定値のままにします。
    
    2.  **リソース グループ** セクションで、リストから **ポリグロットデータ** を選択します。
    
    3.  **ストレージ アカウント** **名** テキスト ボックスに、**polystor\[名前を小文字で入力\]** と入力します。
    
    4.  **場所** ドロップダウン リストで、 **米国東部** リージョンを選択します。
    
    5.  **パフォーマンス** セクションで、**標準** を選択します。   
    
    6.  **アカウントの種類** ドロップダウン リストで、**StorageV2 (汎用 v2)を選択します。*
    
    7.  **レプリケーション** ドロップダウン リストで、**ローカル冗長ストレージ (LRS)** を選択します。
    
    8.  **アクセス層 (既定)** セクションで、**Hot ** が選択されていることを確認します。 
    
    9.  **レビュー + 作成** を選択します。

7.  **レビュー + 作成** タブで、前の手順で選択したオプションを確認します。

8.  指定した構成を使用してストレージ アカウントを作成するには、**作成** を選択します。

9.  演習を進める前に、作成タスクが完了するまで待ちます。

10. Azureポータルの左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーションペインをクリックしてください。

11. **すべてのサービス** ブレードで、**ストレージ アカウント** を選択します。

12. **ストレージ アカウント** ブレードで、プレフィックス **polystor** を持つAzure Storage アカウント インスタンスを選択します。 

13. **ストレージ アカウント** ブレードで、ブレードの左側にある **設定** セクションを見つけ、**アクセスキー** リンクを選択 します。

14. **アクセス キー** ブレードで、いずれかのキーを選択し、**接続文字列** テキスト ボックスに値を記録します。 これらの値は、この演習の後半で使用します。

#### 復習

このエクササイズでは、polyglot データ ソリューションに必要な全ての Azure のリソースを作成しました。

### エクササイズ 2: ASP.NETコアWeb アプリケーションを開いて構成する

#### タスク 1: Web アプリケーションを開く

1.  **スタート** 画面で、**Visual Studio コード** タイルを選択します。

2.  **ファイル** メニューで、**フォルダを開く** を選択します。   

3.  開くファイル エクスプローラー ウインドウで、**すべてのファイル (F):Labfiles\\スターター** に移動し、**フォルダの選択** を選択します。 

#### タスク 2: アプリケーション設定の更新

1.  Visual Studio コード ウインドウの **エクスプローラー** ペインで、**Contoso.Events.Web** プロジェクトを展開 します。   

2.  **エクスプローラー** ペインで、**appsettings.json** を二重選択します。   

3.  JSON オブジェクトの13行目で、 **ConnectionStrings.EventsContextConnectionString** つけます。  現在値が空であることを確認します：

<!-- end list -->

    "ConnectionStrings": {
    "EventsContextConnectionString": ""
    },

4.  この演習で前に記録した **SQL データベース** の **接続文字列** に値を設定して、**EventsContextConnectionString** プロパティの値を更新します。     

5.  JSON オブジェクトの9行目で、**CosmosSettings.EndpointUrl** パスを見つけます。 現在値が空であることを確認します：

<!-- end list -->

    "CosmosSettings": {
    "DatabaseId": "EventsDatabase ",
    "CollectionId": "RegistrationCollection",
    "EndpointUrl": "",
    "AuthorizationKey": ""
    },

6.  この演習で前に記録した**Azure Cosmos DB アカウント** の **エンドポイント URI** に値を設定して、 **EndpointUrl** プロパティの値を更新します。     

7.  JSON オブジェクトの10行目で **CosmosSettings.AuthorizationKey** パスを見つけます。  現在値が空であることを確認します：

<!-- end list -->

    "CosmosSettings": {
    "DatabaseId": "EventsDatabase ",
    "CollectionId": "RegistrationCollection",
    "EndpointUrl": "",
    "AuthorizationKey": ""
    },

8.  このラボで前に記録した **Azure Cosmos DB アカウント** の **キー** に値を設定して、 **AuthorizationKey** プロパティの値を更新します。     

9.  **appsettings.json** ファイルを保存します。

10. Visual Studio コード ペインの **エクスプローラー** ウインドウで、 **Contoso.Events.Worker** プロジェクトを展開します。 

11. **エクスプローラー** ウインドウで、 **local.settings.json** を二重選択します。   

12. JSON オブジェクトの4行目で **AzureWebJobsStorage** パスを見つけます。現在値が空であることを確認します：

<!-- end list -->

    "AzureWebJobsStorage": "",	

13. このラボで前に記録した **ストレージ アカウント** の **接続文字列** に値を設定して、**AzureWebJobsStorage** プロパティの値を更新します。     

14. JSON オブジェクトの5行目で **AzureWebJobsDashboard** パスを見つけます。現在値が空であることを確認します：

<!-- end list -->

    "AzureWebJobsDashboard": "",

15. このラボで前に記録した **ストレージ アカウント** の **接続文字列** に値を設定して、**AzureWebJobsDashboard** プロパティの値を更新します。     

16. JSON オブジェクトの6行目で **EventsContextConnectionString** パスを見つけます。 現在値が空であることを確認します：

<!-- end list -->

    "EventsContextConnectionString": "",

17. この演習で前に記録した **SQL データベース**の**接続文字列** に値を設定して、 **EventsContextConnectionString** プロパティの値を更新します。     

18. JSON オブジェクトの7行目で **CosmosEndpointUrl** パスを見つけます。 現在値が空であることを確認します：

<!-- end list -->

    "CosmosEndpointUrl": "",

19. この演習で前に記録した **Azure Cosmos DB アカウント** の **エンドポイント Uri** に値を設定して、**CosmosEndpointUrl** プロパティの値を更新します。     

20. JSON オブジェクトの8行目で、 **CosmosAuthorizationKey** パスを見つけます。 現在値が空であることを確認します：

<!-- end list -->

    "CosmosAuthorizationKey": "",

21. このラボで前に記録した **Azure Cosmos DB アカウント** の **キー** に値を設定して、 **CosmosAuthorizationKey** プロパティの値を更新します。     

22. **local.settings.json** ファイルを保存します。

#### 復習

この演習では、Azure のリソースに接続するようにASP.NET Core Webアプリケーションを構成しました。

### エクササイズ 3: Azure SQLデータベースに接続するためのエンティティ フレームワーク コードの作成

#### タスク 1: データベース初期化ロジックの構成

1.  Visual Studio コード ウインドウの エクスプローラー ペインで、**Contoso.Events.Data** プロジェクトを展開します。

2.  エクスプローラー** ** ペインで、**ContextInitializer.cs** を二重選択します。   

3.  **InitializeAsync** メソッドを見つけます。

<!-- end list -->

    public async Task InitializeAsync(EventsContext eventsContext)

4.  **InitializeAsync** メソッド内で次のコード行を追加して、データベースが確実に作成されるようにします。 

<!-- end list -->

    await eventsContext.Database.EnsureCreatedAsync();

5.  データベースにイベントがない場合にのみブロック内でコードを実行する条件付き **if** ブロックを作成するには、次のコード ブロックを追加します。

<!-- end list -->

    if (!await eventsContext.Events.AnyAsync())
    {
    }

6.  新しく作成された **if** ブロック内に、次のコード行を追加して **イベント** クラスの新しいインスタンスを作成 します。

<!-- end list -->

    Event eventItem = new Event();

7.  **if** ブロック内に、次のコード ブロックを追加して、新しい **イベント** クラス インスタンスのさまざまなプロパティを設定します:   

<!-- end list -->

    eventItem.EventKey = "FY17SepGeneralConference";
    eventItem.StartTime = DateTime.Today;
    eventItem.EndTime = DateTime.Today.AddDays(3d);
    eventItem.Title = "FY17 September Technical Conference";
    eventItem.Description = "Sed in euismod mi.";
    eventItem.RegistrationCount = 1;

8.  **if**ブロック内に次のコード行を追加して、 新しい **イベント** クラス インスタンスを **DbSet\<Event\>** 型の **イベント** プロパティに追加します。 

<!-- end list -->

    eventsContext.Events.Add(eventItem);

9.  **if ** ブロックの外側と後に次のコード行を追加して、変更をデータベース コンテキストに保存します。

<!-- end list -->

    await eventsContext.SaveChangesAsync();

10. **InitializeAsync** メソッドは次のようになります。 

<!-- end list -->

    public async Task InitializeAsync(EventsContext eventsContext)
    {
    await eventsContext.Database.EnsureCreatedAsync();
    
    if (!await eventsContext.Events.AnyAsync())
    {
    Event eventItem = new Event();
    eventItem.EventKey = "FY17SepGeneralConference";
    eventItem.StartTime = DateTime.Today;
    eventItem.EndTime = DateTime.Today.AddDays(3d);
    eventItem.Title = "FY17 September Technical Conference";
    eventItem.Description = "Sed in euismod mi.";
    eventItem.RegistrationCount = 1;
    eventsContext.Events.Add(eventItem);
    }
    
    await eventsContext.SaveChangesAsync();
    }

11. **ContextInitializer.cs** ファイルを **保存** します。

#### タスク 2: データベースの初期化の更新

1.  Visual Studio コード ウインドウの エクスプローラ ウインドウで、**Contoso.Events.Data** プロジェクトを展開します。

2.  エクスプローラー** ** ペインで、**ContextInitializer.cs** を二重選択します。

3.  **InitializeAsync** メソッドを見つけます。

<!-- end list -->

    public async Task InitializeAsync(EventsContext eventsContext)

4.  Replace the method with the following method implementation:

<!-- end list -->

    public async Task InitializeAsync(EventsContext eventsContext)
    {
    await eventsContext.Database.EnsureCreatedAsync();
    
    if (!await eventsContext.Events.AnyAsync())
    {
    await eventsContext.Events.AddRangeAsync(
    new List<Event>() 
    {
    new Event { EventKey = "GeneralConferenceAlpha", StartTime = DateTime.Today, EndTime = DateTime.Today.AddDays(5d), Title = "First General Conference", Description = "Sed in euismod mi.", RegistrationCount = 15 },
    new Event { EventKey = "GeneralConferenceBravo", StartTime = DateTime.Today.AddDays(10d), EndTime = DateTime.Today.AddDays(15d), Title = "Second General Conference", Description = "Sed in euismod mi.", RegistrationCount = 20 },
    new Event { EventKey = "GeneralConferenceCharlie", StartTime = DateTime.Today.AddDays(20d), EndTime = DateTime.Today.AddDays(25d), Title = "Third General Conference", Description = "Sed in euismod mi.",  RegistrationCount = 5 },
    new Event { EventKey = "GeneralConferenceDelta", StartTime = DateTime.Today.AddDays(30d), EndTime = DateTime.Today.AddDays(35d), Title = "Fourth General Conference", Description = "Sed in euismod mi.", RegistrationCount = 25 },
    new Event { EventKey = "GeneralConferenceEcho", StartTime = DateTime.Today.AddDays(40d), EndTime = DateTime.Today.AddDays(45d), Title = "Fifth General Conference", Description = "Sed in euismod mi.", RegistrationCount = 10 },
    new Event { EventKey = "GeneralConferenceFoxtrot", StartTime = DateTime.Today.AddDays(50d), EndTime = DateTime.Today.AddDays(55d), Title = "Sixth General Conference", Description = "Sed in euismod mi.", RegistrationCount = 0 }
    }
    );
    
    await eventsContext.SaveChangesAsync();
    }
    }

5.  **ContextInitializer.cs** ファイルを **保存** します。

#### タスク 3: ASP.NET MVC コントローラでエンティティ フレームワーク クエリを書き込む

1.  Visual Studio コード ウインドウの エクスプローラー** **ペインで、 **Contoso.Events.Web** プロジェクトを展開します。   

2.  エクスプローラ ペインで、**コントローラー** フォルダを展開します。

3.  エクスプローラー ** ** ペインで、**HomeController.cs** を二重選択します。   

4.  **インデックス** メソッドを見つける:

<!-- end list -->

    public IActionResult Index([FromServices] EventsContext eventsContext, [FromServices] IOptions<ApplicationSettings> appSettings)

5.  **インデックス** メソッド内で、次のコード行を見つけます。 

<!-- end list -->

    var upcomingEvents = Enumerable.Empty<Event>();

6.  そのコード行を次のコード ブロックに置き換えて **イベント** テーブルを照会し、**StartTime** プロパティで結果を並べ替え、アプリケーション設定に基づいて結果のサブセットを取得します。   

<!-- end list -->

    var upcomingEvents = eventsContext.Events
    .Where(e => e.StartTime >= DateTime.Today)
    .OrderBy(e => e.StartTime)
    .Take(appSettings.Value.LatestEventCount);

7.  **HomeController.cs** ファイルを **保存** します。

8.  エクスプローラー** **ペインで、**EventsController.cs** を二重選択します。   

9.  **インデックス** メソッドを見つける:

<!-- end list -->

    public IActionResult Index([FromServices] EventsContext eventsContext, [FromServices] IOptions<ApplicationSettings> appSettings, int? page)

10. **インデックス** メソッド内で、次のコード行を見つけます。

<!-- end list -->

    var pagedEvents = Enumerable.Empty<Event>();

11. そのコード行を次のコード ブロックに置き換えて **イベント** テーブルを照会し、**Skip** メソッドと **Take** メソッドを使用して、現在のページ番号に基づいて結果のページを作成します。     

<!-- end list -->

    int currentPage = page ?? 1;
    int totalRows = eventsContext.Events.Count();
    int pageSize = appSettings.Value.GridPageSize;
    var pagedEvents = eventsContext.Events
    .OrderByDescending(e => e.StartTime)
    .Skip(pageSize * (currentPage - 1))
    .Take(pageSize);

12. **インデックス** メソッド内で、次のコード ブロックを見つけます。 

<!-- end list -->

    EventsGridViewModel viewModel = new EventsGridViewModel
    {
    CurrentPage = 0,
    PageSize = 0,
    TotalRows = 0,
    Events = pagedEvents
    };	

13. そのコード ブロックを次のコード ブロックに置き換えて、**EventsGridViewModel** クラス インスタンスのさまざまなプロパティを設定します。

<!-- end list -->

    EventsGridViewModel viewModel = new EventsGridViewModel
    {
    CurrentPage = currentPage,
    PageSize = pageSize,
    TotalRows = totalRows,
    Events = pagedEvents
    };

14. **詳細** メソッドを見つける:

<!-- end list -->

    public IActionResult Detail([FromServices] EventsContext eventsContext, string key)

15. **詳細** メソッド内で、次のコード行を見つけます。 

<!-- end list -->

    var matchedEvent = default(Event);

16. そのコード行を次のコード ブロックに置き換えて、**イベントキー** プロパティに一致する単一のレコードの **イベントキー** テーブルを照会します。

<!-- end list -->

    var matchedEvent = eventsContext.Events
    .SingleOrDefault(e => e.EventKey == key);

17. **EventsController.cs** ファイルを **保存** します。

#### 復習

この演習では、Entity Frameworkを使用して Azure SQLデータベースに接続するための C\# コードを記述しました。

### エクササイズ 4: Azure Cosmos DBに接続するための Cosmos DBクライアント ライブラリ コードのオーサリング

#### タスク 1: Azure Functionsプロジェクトで登録者名を取得する

1.  Visual Studio コード ウインドウの エクスプローラー ペインで、**Contoso.Events.Worker** プロジェクトを展開 し、 **ProcessDocuments.cs** ファイルを二重選択します。

2.  **ProcessDocuments.cs** ファイルのコード エディタタブで、 **ProcessDocuments** クラスを見つけます。 

<!-- end list -->

    public static class ProcessDocuments

3.  **ProcessDocuments** クラス内で、19行目に新しいコード行を追加して、**RegistrationContext** クラスの新しい静的インスタンスを作成します。

<!-- end list -->

    private static RegistrationContext _registrationsContext = _connection.GetCosmosContext();

4.  **ProcessHttpRequestMessage** メソッドを見つける:

<!-- end list -->

    private static async Task<List<string>> ProcessHttpRequestMessage(string eventKey)

5.  **ProcessHttpRequestMessage** メソッド内で、40行目に新しいコード行を追加して、**RegistrationContext** クラスの **ConfigureConnectionAsync** メソッドを使用してAzure Cosmos DBへの接続を構成します。

<!-- end list -->

    await _registrationsContext.ConfigureConnectionAsync();

6.  **登録者** 変数に文字列値の空のコレクションを格納する41行目のコード行を見つけます。

<!-- end list -->

    List<string> registrants = new List<string>();

7.  41行目のコード行を、**RegistrationContext** クラスの **GetRegistrantsForEvent** メソッドを呼び出す新しいコード行に置き換えます。

<!-- end list -->

    List<string> registrants = await _registrationsContext.GetRegistrantsForEvent(eventKey);

8.  **ProcessDocuments.cs** ファイルを保存します。

#### タスク 2: RegistrationContext クラスの実装

1.  Visual Studio コード ウインドウの エクスプローラー** ** ペインで、**Contoso.Events.Data** プロジェクトを展開し、**RegistrationContext.cs** ファイルを二重に選択します。

2.  **RegistrationContext.cs** ファイルのコード エディタ タブで、**RegistrationContext** クラスを見つけます。 

<!-- end list -->

    public class RegistrationContext

3.  **RegistrationContext** クラス内で新しいコード行を追加して、**データベース** 型の新しいプロパティを作成します。

<!-- end list -->

    protected Database Database { get; set; }

4.  **RegistrationContext** クラス内で新しいコード行を追加して **DocumentCollection** 型の新しいプロパティを作成します。 

<!-- end list -->

    protected DocumentCollection Collection { get; set; }

5.  **RegistrationContext** クラス内で、**DocumentClient** 型の新しいプロパティを作成する新しいコード行を追加します。

<!-- end list -->

    protected DocumentClient Client { get; set; }

6.  **RegistrationContext** クラス内で、既存の **RegistrationContext** コ ンストラクタを見つけます。 

<!-- end list -->

    public RegistrationContext(IOptions<CosmosSettings> cosmosSettings)
    {
    CosmosSettings = cosmosSettings.Value;
    }

7.  コンストラクタ内で、新しいコード行を追加して新しい **DocumentClient** インスタンスを作成 し、それを *Client* プロパティに保存 します。   

<!-- end list -->

    Client = new DocumentClient(new Uri(CosmosSettings.EndpointUrl), CosmosSettings.AuthorizationKey);

8.  **RegistrationContext** クラス内で、**ConfigureConnectionAsync** メソッドを見つけて、メソッド内の既存のコードを削除します。

<!-- end list -->

    public async Task ConfigureConnectionAsync()
    {
    
    }

9.  **ConfigureConnectionAsync** メソッド内で新しい **データベース** インスタンスを作成し、**データベース** プロパティに保存する新しいコード行を追加します。 

<!-- end list -->

    Database = await Client.CreateDatabaseIfNotExistsAsync(new Database { Id = CosmosSettings.DatabaseId });

10. 新しいコード行を追加して、新しい **DocumentCollection** インスタンスを作成 し、それを **Collection** プロパティに保存します。

<!-- end list -->

    Collection = await Client.CreateDocumentCollectionIfNotExistsAsync(Database.SelfLink, new DocumentCollection { Id = CosmosSettings.CollectionId });

11. **RegistrationContext** クラス内で、**GetRegistrantCountAsync** メソッドを見つけて、メソッド内の既存のコードを削除します。

<!-- end list -->

    public async Task<int> GetRegistrantCountAsync()
    {
    
    }

12. **GetRegistrantCountAsync** メソッド内で、**EnableCrossPartitionQuery** プロパティがtrueの値に設定された **FeedOptions** クラスの新しいインスタンスを作成するための新しいコード行を追加します。 

<!-- end list -->

    FeedOptions options = new FeedOptions { EnableCrossPartitionQuery = true };

13. 新しいコード行を追加して、登録者の数を取得し、整数値のコレクションを返すクエリを作成します。

<!-- end list -->

    IDocumentQuery<int> query = Client.CreateDocumentQuery<int>(Collection.SelfLink, "SELECT VALUE COUNT(1) FROM registrants", options).AsDocumentQuery();

14. **IDocumentQuery\<\>** クラスの **HasMoreResults** プロパティを反復し***count** *変数の最終値を返すwhileループである、***count*** という名前の整数変数を作成すべく、コードの新しいブロックを追加します。

<!-- end list -->

    int count = 0;
    while (query.HasMoreResults)
    {
    
    }
    return count;

15. whileループ内で、**IDocumentQuery\<\>** クラスの**ExecuteNextAsync\<\>** メソッドを呼び出すコード行を追加 し、その結果を**FeedResponse\<\>** という種別の***results** *という名前の変数に格納します。

<!-- end list -->

    FeedResponse<int> results = await query.ExecuteNextAsync<int>();

16. while ループ内で、***result*** 変数に 格納されているコレクションに **Sum** LINQ メソッドを呼び出した結果、***count*** 変数を増分するコード行を追加します。

<!-- end list -->

    count += results.Sum();

17. **RegistrationContext** クラス内で、**GetRegistrantsForEvent** メソッドを見つけて、メソッド内の既存のコードを削除します。

<!-- end list -->

    public async Task<List<string>> GetRegistrantsForEvent(string eventKey)
    {
    
    }

18. **GetRegistrantsForEvent** メソッド内で、***eventKey*** パラメータの値を使用して特定のイベントの登録者を取得するためにLINQを使用するコード行を追加し、**GeneralRegistration** クラスを使用してそれらの登録者を逆シリアル化します。

<!-- end list -->

    IDocumentQuery<GeneralRegistration> query = Client.CreateDocumentQuery<GeneralRegistration>(Collection.SelfLink).Where(r => r.EventKey == eventKey).AsDocumentQuery();

19. **IDocumentQuery\<\>** クラスの **HasMoreResults** プロパティを反復し***registrants***** 変数の最終値を返すwhileループである、 ***registrants*** という名前の **List\<\>** 変数を作成すべく、コードの新しいブロックを追加します。

<!-- end list -->

    List<string> registrants = new List<string>();
    while (query.HasMoreResults)
    {
    
    }
    return registrants;

20. whileループ内で、**IDocumentQuery\<\>** クラスの **ExecuteNextAsync\<\>** メソッドを呼び出すコード行を追加 し、その結果を **FeedResponse\<\>** という種別の ***results** *という名前の変数に格納します。

<!-- end list -->

    FeedResponse<GeneralRegistration> results = await query.ExecuteNextAsync<GeneralRegistration>();

21. whileループ内で、LINQ **選択** メソッドを呼び出すコード行 を追加して、**GeneralRegistration** クラスの2つのプロパティを単一の文字列として投影し、結果のコレクションを **IEererable\<\>** 型の ***resultNames*** という名前の変数に格納します。      

<!-- end list -->

    IEnumerable<string> resultNames = results.Select(r => $"{r.FirstName} {r.LastName}");

22. whileループ内で、**List\<\>** クラスの **AddRange** メソッドを使用して、**resultNames** コレクションの値を持つ**registrants** コレクションを追加する別のコード行を追加します。

<!-- end list -->

    registrants.AddRange(resultNames);

23. **RegistrationContext** クラス内で、**UploadEventRegistrationAsync** メソッドを見つけて、メソッド内の既存のコードを削除します。

<!-- end list -->

    public async Task<string> UploadEventRegistrationAsync(dynamic registration)
    {
    
    }

24. **UploadEventRegistrationAsync** メソッド内で、**DocumentClient** 型の **クライアント** プロパティの **CreateDocumentAsync** メソッドを呼び出すコード行を追加し、その結果を **ResourceResponse\<Document\>** 型で、***response*** という名前の変数として保存します。このメソッドは、ドキュメントを Azure Cosmos DB にアップロードします。

<!-- end list -->

    ResourceResponse<Document> response = await Client.CreateDocumentAsync(Collection.SelfLink, registration);

25. ドット表記を使用 して、***response*** 変数の **Resource** プロパティ **（Document** の種類）と **Document** インスタンスの **Id** プロパティにアクセスするコードの別の行を追加 します。 現在のメソッドの結果として文字列 **Id** 値を返します。

<!-- end list -->

    return response.Resource.Id;

26. **RegistrationContect..cs** ファイルを保存します。

#### 復習

この演習では、Azure Cosmos DB のドキュメントにアクセスしてクエリするために必要な C\# コードを記述しました。

### エクササイズ 5: Azure Storage に接続するための Azure SDK コードを書く

#### タスク 1: Azure Functions の BLOB トリガーと出力を実装する

1.  Visual Studio コード ウインドウの エクスプローラー** **ペインで、**Contoso.Events.Worker** プロジェクトを展開 し、**ProcessDocuments.cs** ファイルを二重選択します。

2.  **ProcessDocuments.cs** ファイルのコード エディタタブで、**ProcessDocuments** クラスを見つけます。

<!-- end list -->

    public static class ProcessDocuments

3.  **ProcessDocuments** クラス内で、**Run** メソッドを見つけます。

<!-- end list -->

    public static async Task Run(Stream input, string name, Stream output, TraceWriter log)

4.  *bLobTrigger *パラメータ属性を *input *パラメータに追加して、 **signinsheets-pending** コンテナ内の任意の BLOB に一致するように指定して、**Run** メソッドのメソッドシグネチャを更新します。

<!-- end list -->

    public static async Task Run([BlobTrigger("signinsheets-pending/{name}")] Stream input, string name, Stream output, TraceWriter log)

5.  関数をトリガーした BLOB と同じ名前の **signinsheets** コンテナに新しい BLOB を作成することを指定する *output* パラメータに *Blob* パラメータ属性を追加して、**Run** メソッドのメソッドシグネチャを更新します。実行:       

<!-- end list -->

    public static async Task Run([BlobTrigger("signinsheets-pending/{name}")] Stream input, string name, [Blob("signinsheets/{name}", FileAccess.Write)] Stream output, TraceWriter log)

6.  **Run** メソッド内で、BLOB の名前からファイル拡張子を取り除いて **イベントキー** を取得するには、23行目に新しいコード行を追加します。

<!-- end list -->

    string eventKey = Path.GetFileNameWithoutExtension(name);

7.  **ProcessStorageMessage** メソッドの呼び出しによる **Stream** 結果を使用して **using ブロック** を作成するには、24行目の新しいコード行を追加します。

<!-- end list -->

    using (MemoryStream stream = await ProcessStorageMessage(eventKey))
    {
    
    }

8.  **using** ブロック内に、ストリームの **ToArray** メソッドを呼び出して、**byte\[\]** 型の新しい変数を作成する新しいコード行を追加します。

<!-- end list -->

    byte[] byteArray = stream.ToArray();

9.  **using** ブロック内に、*byteArra y*変数に関連するさまざまなメタデータを渡す*出力*変数の **WriteAsync** メソッドを呼び出す別のコード行を追加します。

<!-- end list -->

    await output.WriteAsync(byteArray, 0, byteArray.Length);

10. **ProcessDocuments.cs** ファイルを保存します。

#### タスク 2: BLOBContextクラスでBLOBアップロードを実装する

1.  Visual Studio コード ウインドウの エクスプローラー ペインで、**Contoso.Events.Data** プロジェクトを展開し、**BlobContext.cs** ファイルを二重選択します。

2.  **BlobContext.cs** ファイルのコードエディタタブで、**BlobContext** クラスを見つけます。 

<!-- end list -->

    パブリック クラス BlobContext

3.  **BlobContext** クラス内で、**UploadBlobAsync** メソッドを見つけて、メソッド内の既存のコードを削除します。

<!-- end list -->

    public async Task<ICloudBlob> UploadBlobAsync(string blobName, Stream stream)
    {
    
    }

4.  **UploadBlobAsync** メソッド内で、新しいコード行を追加して、新しい **CloudStorageAccount** クラス インスタンスを作成します。

<!-- end list -->

    CloudStorageAccount account = CloudStorageAccount.Parse(StorageSettings.ConnectionString);

5.  **CloudStorageAccount** クラスの **CreateCloudBlobClient** メソッドを使用して、**CloudBlobClient** クラスの新しいインスタンスを作成するための新しいコード行を追加します。

<!-- end list -->

    CloudBlobClient blobClient = account.CreateCloudBlobClient();

6.  **CloudBlobClient** クラスの **GetContainerReference** メソッドを使用して、新しいコンテナまたは既存のコンテナへの参照を取得する新しいコード行を追加します。

<!-- end list -->

    CloudBlobContainer container = blobClient.GetContainerReference($"{StorageSettings.ContainerName}-pending");

7.  コンテナーが存在しない場合にコンテナーを作成する **CloudBlobContainer** クラスの **CreateIfNotExistsAsync** メソッドを呼び出す新しいコード行を追加します。

<!-- end list -->

    await container.CreateIfNotExistsAsync();

8.  指定した BLOB 名を使用して、新しい BLOB または既存の BLOB への参照を取得する新しいコード行を追加します。

<!-- end list -->

    ICloudBlob blob = container.GetBlockBlobReference(blobName);

9.  新しいコード行を追加して ***stream*** パラメータを受け取り、ストリームを元に戻します。

<!-- end list -->

    stream.Seek(0, SeekOrigin.Begin);

10. ***stream*** パラメータのコンテンツを参照されるBLOBにアップロードする新しいコード行を追加します。

<!-- end list -->

    await blob.UploadFromStreamAsync(stream);

11. メソッドの結果として更新された BLOB を返す新しいコード行を追加します。

<!-- end list -->

    return new DownloadPayload { Stream = stream, ContentType = blob.Properties.ContentType }; 

12. **Blobcontext.cs** ファイルを **保存** します。

#### 復習

この演習では、Azure Function で Azure Storage BLOB を操作するための C\# コードを記述しました。

### エクササイズ 6: サブスクリプションのクリーンアップ 

#### タスク 1: Azure Cloud Shell を開く

1.  ポータルの上部で、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。

2.  ポータルの下部にある **Cloud Shell** コマンド プロンプトで次のコマンドを入力し、Enter キーを押してサブスクリプション内のすべてのリソース グループを一覧表示します。

<!-- end list -->

    az group list

3.  プロンプトで次のコマンドを入力し、Enter キーを押して、リソース グループを削除する可能性のあるコマンドの一覧を表示します。

<!-- end list -->

    az group delete --help

#### タスク 2: リソース グループを削除する

1.  プロンプトで次のコマンドを入力し、Enter キーを押して **PolyglotData** リソース グループを削除します。

<!-- end list -->

    az group delete --name PolyglotData --no-wait --yes

2.  ポータルの下部にある **Cloud Shell** ペインを閉じます。

#### タスク 3: アクティブなアプリケーションを閉じる

1.  現在実行中の **Microsoft Edge** アプリケーションを閉じます。

2.  現在実行中の **Visual Studio Code** アプリケーションを閉じます。

#### 復習

この実習では、この演習で使用する **リソース グループ** を削除してサブスクリプションをクリーンアップしました。
