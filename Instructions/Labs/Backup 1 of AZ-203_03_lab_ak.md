---
lab:
    title: 'ラボ: ポリグロットデータソリューションの構築'
    type: 'Answer Key'
    module: 'モジュール 3: Azure storage 向けの開発'
---

# ラボ: ポリグロット データ ソリューションの構築
# 受講者ラボ解答キー

## Microsoft Azure ユーザー インターフェイス

Microsoft クラウド ツールのダイナミックな性質を考えると、このトレーニング コンテンツの開発後に Azure ユーザー インターフェイス (UI) の変更が発生する可能性があります。これらの変更により、ラボの指示と手順が正しく一致しない場合があります。

Microsoft は、コミュニティが必要な変更を行うとすぐに、このトレーニング コースを更新します。しかし、クラウド更新が頻繁に起きるため、この研修内容が更新される前に、UI の変更を経験するかも知れません。**その場合は変更に順応して、必要に応じてラボでをそれを処理してください。**

## 指示

### 開始する前に

#### ラボの仮想マシンへのサインイン

次の認証情報を使用して**Windows 10**仮想マシンにサインインします。
    
-   **ユーザー名**: Admin

-   **パスワード**: Pa55w.rd

> **注記**：ラボ仮想マシンのサインイン手順は、インストラクターから提供されます。

#### インストールされたアプリケーションの検討

**Windows 10** デスクトップの下部にあるタスク バーを確認します。タスク バーには、このラボで使用するアプリケーションのアイコンが含まれています。
    
-   Microsoft Edge

-   エクスプローラ

-   Visual Studio Code

#### 練習用ファイルをダウンロードする

1.  タスク バーで、**Windows PowerShell** アイコンを選択します。

1.  PowerShell コマンド プロンプトで、現在の作業ディレクトリを **Allfiles (F):\\** パスに変更します。

    ```
    cd F:
    ```

1.  コマンド プロンプト内で次のコマンドを入力し、Enter キーを押して、GitHub でホストされている **microsoftlearning/AZ-203-DevelopingSolutionsforMicrosoftAzure** プロジェクトを  **Allfiles (F):\\** ドライブにクローンします。

    ```
    git clone --depth 1 --no-checkout https://github.com/microsoftlearning/AZ-203-DevelopingSolutionsForMicrosoftAzure .
    ```

1.  コマンド プロンプト内で次のコマンドを入力し、**Enter** キーを押 して、**AZ-203T03** ラボを完了するために必要なラボ ファイルをチェックアウトします。

    ```
    git checkout master -- Allfiles/*
    ```

1.  現在実行中の **Windows PowerShell** コマンド プロンプト アプリケーションを閉じます。

### エクササイズ 1: Azure 内にデータベース リソースを作成

#### タスク 1: Azure portal を開く

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザ ウインドウで、**Azure potal** ([portal.azure.com](https://portal.azure.com))に移動します。

1.  Microsoft アカウントの**電子メール アドレス**を入力します。

1.  **次へ** を選択します。

1.  Microsoft アカウントの**パスワード**を入力します。

1.  **サインイン** を選択します。

    > **注記**：**Azure Potal **に初めてサインインする場合は、ポータルのツアーを提供するダイアログ ボックスが表示されます。ツアーをスキップしてポータルの使用を開始するには、**開始**を選択します。

#### タスク 2: Azure Cache for Redis リソースを作成する

1.  Azure Potal の左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーション ペインをクリックしてください。

1.  **すべてのサービス** ブレードで、**Azure Cache for Redis**を選択します。

1.  [Azure Cache for Redis] ブレードで、Redis キャッシュ インスタンスの一覧を表示します。 

1.  **Azure Cache for Redis** ブレードの上部にある**+ 追加**を選択します。

1.  **新しい Redis Cache**ブレードで、次の操作を実行します。

    1.  **DNS 名** フィールドに、値 **polyrediscache\[名前を小文字で入力\]** と入力します。 

    1.  **サブスクリプション**ドロップダウン リストは既定値に設定したままにします。
    
    1.  **リソース グループ** セクションで、**新規作成**を選択し、**PolyglotData**を入力し、**OK**を選択します。
    
    1.  **場所** ドロップダウン リストで、**米国東部**オプションを選択します。

    1.  [**価格レベル**] ボックスの一覧で、[**Basic C0 (250MB Cache)**] オプションを選択します。   

    1.  [**ポート 6379 のブロック解除 (SSL 暗号化なし)**]セクションで、チェックボックスが選択されていないことを確認します。 
    
    1. [**作成**] を選択します。

1.  演習を進める前に、作成タスクが完了するまで待ちます。

    > **注記**：Azure Cache for Redis リソースは、**15 ~ 30 分**すると使用できる状態になります。  演習を進めることも可能ですが、**エクササイズ 6** では、このリソースとその接続文字列が必要であることに注意してください。**Azure Redis Cache に接続するための .NET コードの作成**。

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ**リンクを選択します。

1.  **リソース グループ** ブレードで、 この実習ラボで前に作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、この実習ラボで前に作成した **polyrediscache\** Azure Cache for Redis インスタンスを選択します。

1.  **Azure Cache for Redis** ブレードで、ブレードの左側にある**設定**セクションを見つけ、**アクセス キー**リンクを選択 します。

1.  [**アクセス キー**] ウィンドウで、[**一次接続文字列 (StackExchange.Redis)**] フィールドに値を記録します。これらの値は、この演習の後半で使用します。

#### タスク 3: Azure SQL Server リソースを作成する

1.  Azure Potal の左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーション ペインをクリックしてください。

1.  **すべてのサービス**ブレードで、**SQLサーバー**を選択します。

1.  **SQLサーバー**ブレードで、SQL サーバー インスタンスの一覧を表示します。

1.  **SQLサーバー**ブレードの上部にある**+ 追加**を選択します。

1.  **SQL Database Server の作成**ブレードで、**基本**、**ネットワーク**および**追加設定**などのタブをブレードの上部にあるタブに従います。

    > **注記**: 各タブは、新しい **Azure SQL Database サーバー**を作成するためのワークフローのステップを表します。いつでも**レビュー + 作成**を選択して、残りのタブをスキップできます。

1.  **基本**タブで、次の操作を実行します：
    
    1.  **サブスクリプション**ドロップダウン リストは既定値に設定したままにします。
    
    1.  **リソース グループ** セクションで、リストから**ポリグロットデータ**を選択します。
    
    1.  **サーバー名** フィールドに、値**polysqlsrvr\[名前を小文字で入力\]**と入力します。
    
    1.  **場所** ドロップダウン リストで、**(US) 米国東部**オプションを選択します。
    
    1.  **サーバー管理者ログイン** フィールドに、値 **testuser**を入力します。
    
    1.  **パスワード**フィールドに、値**TestPa$$w0rd**.を入力します。
    
    1.  **パスワードの確認** フィールドに、値**TestPa$$w0rd**をもう一度入力します。

    1.  **次へ** 選択します:** ネットワーク >**。

1.  **ネットワーク** タブで、次の操作を実行します：

    1. [**Azure のサービスとリソースにこのサーバーへのアクセスを許可する**] セクションで、[**はい**]を選択します。   
    
    1.  **レビュー + 作成**を選択します。

1.  **レビュー + 作成**タブで、前の手順で選択したオプションを確認します。

1.  指定した構成を使用して SQL Database サーバーを作成するには、**作成**を選択します。

1.  演習を進める前に、作成タスクが完了するまで待ちます。

#### タスク 4: Azure Cosmos DB アカウント リソースの作成

1.  Azure potalの左側にあるナビゲーションペインで、**すべてのサービス**ナビゲーションペインをクリックしてください。

1.  **すべてのサービス** ブレードで、**Azure コスモス DB**を選択します。

1.  **Azure コスモス DB**ブレードで、Azure Cosmos DB インスタンスの一覧を表示します。

1.  **Azure Cosmos DB**ブレードの上部にある**+ 追加**を選択します。

1.  **Azure Cosmos DB アカウントの作成** ブレードで、**基本**、**ネットワーク**および**タグ**などのブレードの上部にあるタブを確認します。

    > **注記**: 各タブは、ワークフロー内の新しい**Azure Cosmos DB アカウント**を作成するためのステップを表します。いつでも**レビュー + 作成**を選択して、残りのタブをスキップできます。

1.  **基本**タブで、次の操作を実行します：
    
    1.  **サブスクリプション** リストは既定値に設定したままにします。
    
    1.  **リソース グループ** セクションで、リストから**ポリグロットデータ**を選択します。
    
    1.  **AccountName**フィールド に、**polycosmos\[小文字で名前を指定\]**と入力します。
    
    1.  **API** ドロップダウン リストで、**コア (SQL)**オプションを選択します。
    
    1.  **場所** ドロップダウン リストで、 **米国東部**リージョンを選択します。
    
    1.  **地理冗長性** セクションで、**無効にする**オプションを選択します。
    
    1.  **マルチリージョン書き込み**セクションで、**無効**オプションを選択します。
    
    1.  **レビュー + 作成**を選択します。

1.  **レビュー + 作成**タブで、前の手順で選択したオプションを確認します。

1.  指定した構成を使用して Azure Cosmos DB アカウントを作成するには、**作成**を選択します。

1.  演習を進める前に、作成タスクが完了するまで待ちます。

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ**リンクを選択します。

1.  **リソース グループ** ブレードで、 この実習ラボで前に作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した**polycosmos\** Azure Cosmos DB アカウントを選択します。

1.  **Azure Cosmos DB アカウント** ブレードで、 ブレードの左側にある**設定**セクションを見つけて、**キー**リンクを選択します。

1.  [**キー**] ペインで、[ **一次接続文字列**] フィールドに値を記録します。これらの値は、この演習の後半で使用します。

#### タスク 5: Azure Storage  アカウント リソースの作成

1.  Azure potalの左側にあるナビゲーションペインで、**すべてのサービス**ナビゲーションペインをクリックしてください。

1.  **すべてのサービス**ブレードで、**ストレージ アカウント**を選択します。

1.  **ストレージ アカウント**ブレードで、ストレージ インスタンスの一覧を表示します。

1.  **ストレージ アカウント**ブレードの上部にある**+追加**を選択 します。

1.  **ストレージ アカウントを作成**ブレード で、**基本**、**詳細**および**タグ**などのブレードの上部にあるタブを確認します。

    > **注記**: 各タブは、ワークフロー内の新しい**Azure Storage  アカウント**を作成するためのステップを表します。いつでも**レビュー + 作成**を選択して、残りのタブをスキップできます。

1.  **基本**タブで、次の操作を実行します：
    
    1.  **サブスクリプション** リストは既定値に設定したままにします。
    
    1.  **リソース グループ** セクションで、リストから**ポリグロットデータ**を選択します。
    
    1.  **ストレージ アカウント名** フィールドに、**polystor\[小文字で名前を入力\]** と入力します。
    
    1.  **場所** ドロップダウン リストで、 **米国東部**リージョンを選択します。
    
    1.  **パフォーマンス** セクションで、**標準**を選択します。
    
    1.  **アカウントの種類**ドロップダウン リストで、**StorageV2 (汎用 v2)**を選択します。
    
    1.  **レプリケーション** ドロップダウン リストで、**ローカル冗長ストレージ (LRS)**を選択します。
    
    1.  **アクセス層 (既定)**セクションで、**Hot** が選択されていることを確認します。
    
    1.  **レビュー + 作成**を選択します。

1.  **レビュー + 作成**タブで、前の手順で選択したオプションを確認します。

1.  指定した構成を使用してストレージ アカウントを作成するには、**作成**を選択します。

1.  演習を進める前に、作成タスクが完了するまで待ちます。

#### 復習

このエクササイズでは、polyglot データ ソリューションに必要な全ての Azure のリソースを作成しました。

### エクササイズ 2: データベースとイメージのインポート

#### タスク 1: イメージ BLOB のアップロード

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ**リンクを選択します。

1.  **リソース グループ** ブレードで、 この実習ラボで前に作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した**polystor\** ストレージ アカウントを選択します。

1.  **ストレージ アカウント** ブレードで、ブレードの左側にある**Blob service**セクションにある **Containers** リンクを選択します。

1.  **Containers** セクションで、**+ コンテナー**を選択します。

1.  **新規コンテナ**ポップアップで、次の操作を実行します。
    
    1.  **名前**フィールドに、**イメージ**を入力します。
    
    1.  **パブリック アクセス レベル**ドロップダウン リストで、**BLOB (BLOBのみの匿名読み取りアクセス)**を選択します。
    
    1.  **OK** を選択します。

1.  **Containers** セクションに戻 り、新しく作成した **images** コンテナーを選択します。

1.  **コンテナー** ブレードで、ブレードの左側にある**設定**セクションを見つけ、**プロパティ** リンクを選択 します。

1.  [**プロパティ**] ペインで、**URL**フィールドの値を記録します。これらの値は、この演習の後半で使用します。

1.  ブレードの左側にある [**概要**] リンクを見つけて選択します。

1.  ブレードの上部にある**アップロード**をクリックします。

1.  **BLOB をアップロード**ポップアップで、次の操作を実行します。
    
    1.  **ファイル** セクションで、**フォルダ**アイコンを選択します。
    
    1.  ファイル エクスプローラ ダイアログ ボックスで、**すべてのファイル (F):\\Allfiles\\Labs\\03\\Starter**に移動し、42 の **jpg** イメージ ファイルを選択し、**開く**を選択します。
    
    1.  **ファイルが既に存在する場合は、上書き**が選択されていることを確認します。
    
    1.  **アップロード**を選択します。

1. この演習を続行する前に、全ての BLOB がアップロードされるのを待ちます。

#### タスク 2: SQL .bacpac ファイルのアップロード

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ**リンクを選択します。

1.  **リソース グループ** ブレードで、 この実習ラボで前に作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した**polystor\** ストレージ アカウントを選択します。

1.  **ストレージ アカウント** ブレードで、ブレードの左側にある**Blob service**セクションにある **Containers** リンクを選択します。

1.  **Containers** セクションで、**+ コンテナー**を選択します。

1.  **新規コンテナ**ポップアップで、次の操作を実行します。
    
    1.  **名前**フィールドに、**databases** と入力します。
    
    1.  **パブリック アクセス レベル**ドロップダウン リストで、**プライベート(匿名アクセスなし)**を選択します。
    
    1.  **OK** を選択します。

1.  **Containers** セクションに戻 り、新しく作成した **データベース** コンテナーを選択します。

1.  **コンテナ** ブレードで、**アップロード**を選択します。

1.  **BLOB をアップロード**ポップアップで、次の操作を実行します。
    
    1.  **ファイル** セクションで、**フォルダ**アイコンを選択します。
    
    1.  ファイル エクスプローラ ダイアログ ボックスで、**すべてのファイル (F):\\Allfiles\\Labs\\03\\Starter**に移動し、**AdventureWorks.bacpac** ファイルを選択し、**開く**を選択します。
    
    1.  **ファイルが既に存在する場合は、上書き**が選択されていることを確認します。
    
    1.  **アップロード**を選択します。

1. この演習を続行する前に、BLOB がアップロードされるのを待ちます。

#### タスク 3: SQL Database のインポート

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ**リンクを選択します。

1.  **リソース グループ** ブレードで、 この実習ラボで前に作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した**polysqlsrvr\** SQL サーバーを選択します。

1.  **SQL サーバー** ブレードで、[**データベースのインポート**]を選択します 。

1.  表示される **BLOB のインポート** ブレードで、次の操作を実行します：

    1.  **サブスクリプション** リストは既定値に設定したままにします。

    1.  [**ストレージ**] オプションを選択します。 

    1.  表示される**ストレージ アカウント** ブレード で、この実習ラボで作成済みの**polystor\**ストレージ アカウントを選択します。 

    1.  表示される[**コンテナー**]ブレードで、このラボで以前に作成した**データベース** コンテナを選択します 。 

    1.  表示される**コンテナー** ブレード で、このラボで作成した **AdventureWorks.bacpac** BLOB を選択し、[**選択**]を選択してブレードを閉じます。     

    1.  [**データベースのインポート**] ブレードに戻り、[**価格レベル**] オプションを既定値のままにします。   

    1.  **データベース名** フィールドに **AdventureWorks** と入力 します。

    1.  **照合順序**フィールドは既定値に設定したままにします。

    1.  **サーバー管理者ログイン** フィールドに、値 **testuser**を入力します。
    
    1.  **パスワード**フィールドに、値**TestPa$$w0rd**.を入力します。
    
    1.  **OK** を選択します。

1. この演習を続行する前に、データベースが作成されるのを待ちます。

#### タスク 4: インポートされた SQL データベースを使用する

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ**リンクを選択します。

1.  **リソース グループ** ブレードで、 この実習ラボで前に作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した**polysqlsrvr\** SQL サーバーを選択します。

1.  **SQL Server** ブレードで、ブレードの 左側にある**セキュリティ**セクションを見つけ、**ファイアウォールと仮想ネットワーク**リンクを選択します。

1.  [**ファイアウォールと仮想 ネットワーク**] ペインで、[**クライアント IP の追加**] を 選択し、[**保存**] を選択します。     

    > **注記**: この手順により、ローカル コンピュータがこのサーバーに関連付けられたデータベースにアクセスできるようになります。

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ**リンクを選択します。

1.  **リソース グループ** ブレードで、 この実習ラボで前に作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した**AdventureWorks** SQL データベースを選択します。

1.  **SQL データベース** ブレードで、 ブレードの左側にある**設定**セクションを見つけ、**接続文字列**リンクを選択します。

1.  [**接続文字列**] ペインで、[**ADO.NET (SQL 認証)**]フィールドに値を記録します。これらの値は、この演習の後半で使用します。

1.  次の操作を実行して、記録した接続文字列を更新します。

    1.  接続文字列内で ``{your_username}`` プレースホルダを見つけ、``testuser`` に置き換えます。

    1.  接続文字列内で ``{your_password}`` プレースホルダを見つけ、``TestPa$$w0rd`` に置き換えます。

        >**注意**: たとえば、接続文字列がもともと ``Server=tcp:polysqlsrvrinstructor.database.windows.net,1433;Initial Catalog=AdventureWorks;User ID={your_username};Password={your_password};`` である場合、更新された接続文字列は ``Server=tcp:polysqlsrvrinstructor.database.windows.net,1433;Initial Catalog=AdventureWorks;User ID=testuser;Password=TestPa$$w0rd;`` となります。

1.  ブレードの左側にある [**クエリ エディタ**] リンクを見つけて選択します。

1.  **クエリ エディタ** ペインで、次の操作を実行します。

    1.  **ログイン**フィールドに、値**testuser** を入力します。

    1.  **パスワード**フィールドに、値**TestPa$$w0rd**.を入力します。

    1.  **OK** を選択します。

1.  開いているクエリ エディターで、次のクエリを入力します。

    ```
    SELECT * FROM AdventureWorks.dbo.Models
    ```

1.  [**実行**]を選択してクエリを実行します。 

1.  検索クエリの結果を確認します。

    > **注記**: このクエリは、Web アプリのホームページに表示されるモデルの一覧を返します。

1.  クエリ エディターで、既存のクエリを次のクエリに置き換えます。

    ```
    SELECT * FROM AdventureWorks.dbo.Products
    ```

1.  [**実行**]を選択してクエリを実行します。

1.  検索クエリの結果を確認します。

    > **注記**: このクエリは、各モデルに関連付けられている製品の一覧を返します。

#### 確認

この演習では、Web アプリケーションで使用するすべてのリソースをインポートしました。

### エクササイズ 3: .NET コア Web アプリケーションを開いて構成する

#### タスク 1: Web アプリを開いてビルドする

1.  **スタート** 画面で、**Visual Studio コード**タイルを選択します。

1.  **ファイル** メニューで、**フォルダを開く**を選択します。

1.  開くファイル エクスプローラ ウインドウで、**すべてのファイル (F):\\Allfiles\\03\\Starter\\AdventureWorks**に移動し、**フォルダの選択**を選択します。

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注記**: ``dotnet build`` コマンドは、フォルダー内のすべてのプロジェクトをビルドする前に、不足している NuGet パッケージを自動的に復元します。

1.  端末に印刷されたビルドの結果を確認します。問題がなければ、ビルドは正常に完了し、エラーや警告メッセージは表示されません。

1.  [**ゴミ箱**] アイコンを選択して、現在開いている端子と関連するプロセスを破棄します。 

#### タスク 2: SQL 接続文字列の更新

1.  Visual Studio コード ペインの**エクスプローラー** ウインドウで、**AdventureWorks.Web** プロジェクトを展開します。

1.  **appsettings.json** ファイルをダブルクリック (またはダブル選択) します。

1.  JSON オブジェクトの3行目で **ConnectionStrings.AdventureWorksSqlContext** パスを見つけます。現在値が空であることを確認します：

    ```
    "ConnectionStrings": {
        "AdventureWorksSqlContext": "",
        ...
    },
    ```

1.  この演習で前に記録した**SQL データベース** の **ADO.NET（SQL 認証）接続文字列**に値を設定して、**AdventureWorksSqlContext**プロパティの値を更新します。

    > **注記**: ここで、更新された接続文字列を使用することが重要となります。Portal からコピーされた元の接続文字列には、SQL データベースへの接続に必要なユーザー名とパスワードが存在しません。

1.  **appsettings.json**ファイルを保存します。

#### タスク 3: BLOB ベース URL の更新

1.  JSON オブジェクトの8行目で、**Settings.BlobContainerUrl** パスを見つけます。現在値が空であることを確認します：

    ```
    "Settings": {
        "BlobContainerUrl": "",
        ...
    }
    ```

1.  このラボで前に記録した **images** と名付けられた **Azure Storage** BLOB コンテナーの **URL** プロパティに値を設定して、**BlobContainerUrl** プロパティの値を更新します。

1.  **appsettings.json**ファイルを保存します。

#### タスク 4: Web アプリを検証する

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Web** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Web\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注記**: ``dotnet run`` コマンドは、プロジェクトに対するすべての変更を自動的にビルドし、デバッガーをアタッチせずに Web アプリケーションを起動します。このコマンドは、実行中のアプリケーションの URL と割り当てられたポートを出力します。

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、現在実行中の Web アプリケーション (<http://localhost:5000>) に移動します。

1.  Web アプリケーションで、フロント ページに表示されるモデルの一覧を確認します。

1.  **ウォーター ボトル** モデルを見 つけて、[**詳細の表示**] を選択します。   

1.  **ウォーター ボトル** 製品詳細ページで、[**カートに追加**] を選択します。

1.  チェックアウト機能が無効になっていることを確認します。

    > **注記**: 現時点では、製品ページ機能のみが実装されています。チェックアウト ロジックは、このラボの後半で実装します。

1.  Web アプリケーションを表示するブラウザー ウィンドウを閉じます。

1.  **Visual Studio Code** ウィンドウに戻ります。

1.  **Visual Studio Code** ウィンドウに戻り、 **ゴミ箱**アイコンを選択して、現在開いているターミナルと関連プロセスを破棄します。

#### 確認

この演習では、Azure のリソースに接続するようにASP.NET Core Webアプリケーションを構成しました。

### エクササイズ 4: SQL データを Azure Cosmos DB に移行する

#### タスク 1: 移行プロジェクトの作成

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、 **AdventureWorks.Migrate** と名付けられた新しい .NET プロジェクトを同じ名前のフォルダー内に作成します。

    ```
    dotnet new console --name AdventureWorks.Migrate --langVersion 7.1
    ```

    > **注記**: ``dotnet new`` コマンドは、プロジェクトと同じ名前のフォルダーに新しい**コンソール** プロジェクトを作成します。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して、既存の **AdventureWorks.Models** プロジェクトへの参照を追加します。

    ```
    dotnet add .\AdventureWorks.Migrate\AdventureWorks.Migrate.csproj reference .\AdventureWorks.Models\AdventureWorks.Models.csproj
    ```

    > **注記**: ``dotnet add reference`` コマンドは、**AdventureWorks.Models** プロジェクトに含まれるモデル クラスへの参照を追加します。

1.  コマンドプロンプトで次のコマンドを入力し、Enterキーを押して、既存の **AdventureWorks.Context** プロジェクトへの参照を追加します。

    ```
    dotnet add .\AdventureWorks.Migrate\AdventureWorks.Migrate.csproj reference .\AdventureWorks.Context\AdventureWorks.Context.csproj
    ```

    > **注記**: ``dotnet add reference`` コマンドは、**AdventureWorks.Context** プロジェクトに含まれるコンテキスト クラスへの参照を追加します。

1.  コマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Migrate** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Migrate
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して、NuGet から **Microsoft.EntityFrameworkCore.SqlServer** のバージョン **2.2.6** をインポートします 。

    ```
    dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 2.2.6
    ```

    > **注記**: ``dotnet add package`` コマンドは、**NuGet**から **[Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/2.2.6)** パッケージを追加します。

1.  コマンド プロンプトで次のコマンドを入力し、Enterキーを押して、NuGetから現在のプロジェクトに **Microsoft.Azure.Cosmos** の**3.0.0**バージョンをインポートします。

    ```
    dotnet add package Microsoft.Azure.Cosmos --version 3.0.0
    ```

    > **注記**: ``dotnet add package`` コマンドは、**NuGet**から **[Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos/3.0.0)** パッケージを追加します。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  [**ゴミ箱**] アイコンを選択して、現在開いている端子と関連するプロセスを破棄します。

#### タスク 2: .NET クラスの作成 

1.  Visual Studio コード ペインの**エクスプローラー** ウインドウで、**AdventureWorks.Migrate** プロジェクトを展開します。

1.  **Program.cs** ファイルをダブルクリック (またはダブル選択) します。

1.  **Program.cs** ファイルのコード エディタ タブで、既存のファイルのすべてのコードを削除します。

1.  次のコード行を追加して、参照先の **AdventureWorks.Models** および **AdventureWorks.Context** プロジェクトから **AdventureWorks.Models** および **AdventureWorks.Context** 名前空間をインポートします。   

    ```
    using AdventureWorks.Context;
    using AdventureWorks.Models;
    ```

1.  次のコード行を追加して、NuGet からインポートした **Microsoft.Azure.Cosmos** パッケージから **Microsoft.Azure.Cosmos** 名前空間をインポートします。

    ```
    using Microsoft.Azure.Cosmos;
    ```

1.  次のコード行を追加して、NuGetからインポートされた **Microsoft.EntityFrameworkCore.SqlServer** パッケージから **Microsoft.EntityFrameworkCore** 名前空間をインポートします。

    ```
    using Microsoft.EntityFrameworkCore;
    ```

1.  次のコード行を追加して、このファイルで使用される組み込み名前空間の **using** ディレクティブを追加します。

    ```
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  次のコードを入力して、新しい **Program** クラスを作成します。 

    ```
    public class Program
    {
    }
    ```

1.  **Program** クラス内で、次のコード行を入力して、**sqlDBConnectionString** と名付けられた新しい文字列定数を作成します。

    ```
    private const string sqlDBConnectionString = "";
    ```

1.  このラボで以前に記録した **SQL データベース**の**ADO.NET（SQL 認証）接続文字列**に値を設定して、**sqlDBConnectionString** 文字列定数を更新します。

    > **注記**: ここで、更新された接続文字列を使用することが重要となります。Portal からコピーされた元の接続文字列には、SQL データベースへの接続に必要なユーザー名とパスワードが存在しません。

1.  **Program** クラス内で、次のコード行を入力して、**cosmosDBConnectionString** と名付けられた新しい文字列定数を作成します。 

    ```
    private const string cosmosDBConnectionString = "";
    ```

1.  このラボで前に記録した **Azure Cosmos DBアカウント**の **PRIMARY CONNECTION STRING** に値を設定して、**cosmosDBConnectionString** 文字列定数を更新します。

1.  **Program** クラス内に次のコードを入力して、新しい非同期 **Main** メソッドを作成します。

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  **Main** メソッド内で、次のコード行を追加して、概要メッセージをコンソールに出力します。

    ```
    await Console.Out.WriteLineAsync("Start Migration");
    ```

1.  **Program.cs** ファイルを保存します。

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Migrate** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Migrate
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  [**ゴミ箱**] アイコンを選択して、現在開いている端子と関連するプロセスを破棄します。

#### タスク 4: エンティティ フレームワークを使用して SQL データベース レコードを取得する

1.  **Program.cs** ファイル内の **Program** クラスの **Main** メソッド内に、次のコード行を追加して、接続文字列値として **sqlDBConnectionString** 変数をパスする **AdventureWorksSqlContext** クラスの新しいインスタンスを作成します。

    ```
    AdventureWorksSqlContext context = new AdventureWorksSqlContext(sqlDBConnectionString);
    ```

1.  **Main** メソッド内で、次のコードブロックを追加して LINQ クエリを発行し、データベースからすべての**モデル**と子**製品**を取得して、メモリ内の **List<>** コレクションに保存します。

    ```
    List<Model> items = await context.Models
        .Include(m => m.Products)
        .ToListAsync<Model>();
    ```

1.  **Main** メソッド内で、次のコード行を追加して、 **Azure SQL Database** からインポートされたレコードの数を出力します 。

    ```
    await Console.Out.WriteLineAsync($"Total Azure SQL DB Records: {items.Count}");
    ```

1.  **Program.cs** ファイルを保存します。

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Migrate** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Migrate
    ```
    
1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注記**: ビルド エラーがある場合は、**すべてのファイル(F):\\Allfiles\\Labs\\03\\Solution\\AdventureWorks\\AdventureWorks.Migrate** フォルダにある **Program.cs** ファイルを確認してください。

1.  [**ゴミ箱**] アイコンを選択して、現在開いている端子と関連するプロセスを破棄します。

#### タスク 5: Azure Cosmos DB にアイテムを挿入する

1.  **Program.cs** ファイル内の **Program** クラスの **Main** メソッド内に、次のコード行を追加して、接続文字列値として **cosmosDBConnectionString** 変数をパスする **CosmosClient** クラスの新しいインスタンスを作成します。

    ```
    CosmosClient client = new CosmosClient(cosmosDBConnectionString);
    ```

1.  **Main** メソッド内で、次のコード行を追加して、Azure Cosmos DB アカウントに存在しない場合は **Retail** と名付けられた新しい**データベース**を作成します。

    ```
    Database database = await client.CreateDatabaseIfNotExistsAsync("Retail");
    ```

1.  **Main** メソッド内で、次のコードブロックを追加して、**/Category** のパーティション キー パスと **1000 RU** のスループットを有する Azure Cosmos DB アカウントに既に存在しない場合のみ、**Online** という名前の新しい**コンテナー**を作成します。

    ```
    Container container = await database.CreateContainerIfNotExistsAsync("Online",
        partitionKeyPath: $"/{nameof(Model.Category)}",
        throughput: 1000
    );
    ```

1.  **Main** メソッド内で、次のコード行を追加して、**count** と名付けられた **int** 変数を作成します。

    ```
    int count = 0;
    ```

1.  **Main** メソッド内で、次のコードブロックを追加して、 **項目**コレクション内のオブジェクトを反復処理する **foreach** ループを作成します。

    ```
    foreach (var item in items)
    {
    }
    ```

1.  **Main** メソッドに含まれる **foreach** ループ内で、次のコード行を追加してオブジェクトを Azure Cosmos DB コレクションに**アップサート**し、その結果を **document** と名付けられた **ItemResponse<>** タイプの変数に保存します。

    ```
    ItemResponse<Model> document = await container.UpsertItemAsync<Model>(item);
    ```

1.  **Main** メソッドに含まれる **foreach** ループ内で、次のコード行を追加して、各アップサート操作の**アクティビティ ID**を出力します。

    ```
    await Console.Out.WriteLineAsync($"Upserted document #{++count:000} [Activity Id: {document.ActivityId}]");
    ```

1.  **Main** メソッド (foreach ループの外側) に戻り、次のコード行を追加して、**Azure Cosmos DB** にエクスポートされたドキュメントの数を出力します。

    ```
    await Console.Out.WriteLineAsync($"Total Azure Cosmos DB Documents: {count}");
    ```

1.  **Program.cs** ファイルを保存します。

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Migrate** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Migrate
    ```
    
1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注記**: ビルド エラーがある場合は、**すべてのファイル (F):\\Allfiles\\Labs\\03\\Solution\\AdventureWorks\\AdventureWorks.Migrate** フォルダにある **Program.cs** ファイルを確認してください。

#### タスク 6: 移行の実行

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注記**: ``dotnet run`` コマンドはコンソール アプリケーションを起動します。

1.  画面にプリントされるさまざまなデータを確認してください。これには、初期 SQL レコード数、個々のアップサート アクティビティ識別子、最終的な Azure Cosmos DB ドキュメント数などが含まれます。

1.  [**ゴミ箱**] アイコンを選択して、現在開いている端子と関連するプロセスを破棄します。

#### タスク 7: 移行の検証

1.  **Azure Potal** を示す **Microsoft Edge** ブラウザー ウィンドウに戻ります。

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ**リンクを選択します。

1.  **リソース グループ** ブレードで、 この実習ラボで前に作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した**polycosmos\** Azure Cosmos DB アカウントを選択します。

1.  **Azure Cosmos DB アカウント** ブレードで、ブレードの左側にある[**クエリ エクスプローラー**] リンクを見つけて選択します。

1.  [**クエリ エクスプローラー**] ウィンドウで、**Retail** データベースノードを展開します。

1.  [**オンライン**] コンテナー ノードを展開します。 

1.  [**新しい SQL クエリ**] を選択します。 

    > **注記**: このオプションのラベルは非表示になっている可能性があります。[**データエクスプローラー**] ペインの上部にあるアイコンにカーソルを合わせると、ラベルが表示されます。

1.  表示されるクエリ タブで、次のテキストを入力します。

    ```
    SELECT * FROM models
    ```

1.  [**クエリの実行**] を選択します。 

1.  クエリによって返される JSON モデルの一覧を確認します。

1.  クエリ エディタに戻り、既存のテキストを次のテキストに置き換えます。

    ```
    SELECT VALUE COUNT(1) FROM models
    ```

1.  [**クエリの実行**] を選択します。

1.  **COUNT** 集計操作の結果を確認します。

1.  **Visual Studio Code** ウィンドウに戻ります。

#### 確認

この演習では、エンティティ フレームワークと .NET SDK for Azure Cosmos DB を使用して、Azure SQL Database から Azure Cosmos DB にデータを移行しました。

### エクササイズ 5: .NET を使用して Azure Cosmos DB にアクセスする

#### タスク 1: Cosmos SDK および参照を使用してライブラリを更新する

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Context** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Context\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NuGet から **Microsoft.Azure.Cosmos** をインポートします。

    ```
    dotnet add package Microsoft.Azure.Cosmos --version 3.0.0
    ```

    > **注記**: ``dotnet add package`` コマンドは、**NuGet**から **[Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos/3.0.0)** パッケージを追加します。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  [**ゴミ箱**] アイコンを選択して、現在開いている端子と関連するプロセスを破棄します。

#### タスク 2: Azure Cosmos DB に接続する .NET コードを書き込みます。

1.  Visual Studio コード ペインの**エクスプローラー** ウインドウで、**AdventureWorks.Context** プロジェクトを展開します。

1.  コンテキストメニューにアクセスするか、 **AdventureWorks.Context** フォルダーノードを右クリックして、[**新しいファイル**] を選択します。

1.  表示されるプロンプトで、**AdventureWorksCosmosContext.cs** の値を入力します。 

1.  **AdventureWorksCosmosContext.cs** ファイルのコード エディタ タブで、次のコード行を追加して、参照されている **AdventureWorks.Models** プロジェクトから **AdventureWorks.Models** 名前空間をインポートします。

    ```
    using AdventureWorks.Models;
    ```

1.  次のコード行を追加して、NuGet からインポートした **Microsoft.Azure.Cosmos** パッケージから **Microsoft.Azure.Cosmos** と **Microsoft.Azure.Cosmos.Linq** 名前空間をインポートします。

    ```
    using Microsoft.Azure.Cosmos;
    using Microsoft.Azure.Cosmos.Linq;
    ```

1.  次のコード行を追加して、このファイルで使用される組み込み名前空間の **using** ディレクティブを追加します。

    ```
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  次のコードを入力して、**AdventureWorks.Context** 名前空間ブロックを追加します。

    ```
    namespace AdventureWorks.Context
    {
    }
    ```

1.  **AdventureWorks.Context** 名前空間内で、次のコードを入力して、新しい **AdventureWorksCosmosContext** クラスを作成します。

    ```
    public class AdventureWorksCosmosContext
    {
    }
    ```

1.  このクラスが **IAdventureWorksProductContext** インターフェイスを実装することを示す仕様を追加して、**AdventureWorksCosmosContext** クラスの宣言を更新します。

    ```
    public class AdventureWorksCosmosContext : IAdventureWorksProductContext
    {
    }
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のコード行を入力して、**_container** と名付けられた読み取り専用の新しい**コンテナー**変数を作成します。

    ```
    private readonly Container _container;
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のシグネチャを持つ新しいコンストラクターを追加します。

    ```
    public AdventureWorksCosmosContext(string connectionString, string database = "Retail", string container = "Online")
    {
    }
    ```

1.  コンストラクター内で、次のコードブロックを追加して **CosmosClient** クラスの新しいインスタンスを作成し、クライアントから**データベース** インスタンスと**コンテナー** インスタンスの両方を取得します。

    ```
    _container = new CosmosClient(connectionString)
        .GetDatabase(database)
        .GetContainer(container);
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のシグネチャを持つ新しい **FindModelAsync** メソッドを追加します。

    ```
    public async Task<Model> FindModelAsync(Guid id)
    {
    }
    ```

1.  **FindModelAsync** メソッド内で、次のコード ブロックを追加して LINQ クエリを作成し、それを反復子に変換し、結果セットを反復処理して、結果セットの単一のアイテムを返します。

    ```
    var iterator = _container.GetItemLinqQueryable<Model>()
        .Where(m => m.id == id)
        .ToFeedIterator<Model>();

    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches.SingleOrDefault();
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のシグネチャを持つ新しい **GetModelsAsync** メソッドを追加します。

    ```
    public async Task<List<Model>> GetModelsAsync()
    {
    }
    ```

1.  **GetModelsAsync** メソッド内で、次のコードブロックを追加して SQL クエリを実行し、クエリ結果の反復子、結果セットの反復子を取得して、すべての結果の和集合を返します。

    ```
    string query = $@"SELECT * FROM items";

    var iterator = _container.GetItemQueryIterator<Model>(query);

    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches;
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のシグネチャを持つ新しい **FindProductAsync** メソッドを追加します。

    ```
    public async Task<Product> FindProductAsync(Guid id)
    {
    }
    ```

1.  **FindProductAsync** メソッド内で、次のコード ブロックを追加して SQL クエリを実行し、クエリ結果イテレータを取得し、結果セットを反復処理して、結果セットの単一のアイテムを返します。

    ```
    string query = $@"SELECT VALUE products
                        FROM models
                        JOIN products in models.Products
                        WHERE products.id = '{id}'";

    var iterator = _container.GetItemQueryIterator<Product>(query);

    List<Product> matches = new List<Product>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches.SingleOrDefault();
    ```

1.  **AdventureWorksCosmosContext.cs** ファイルを保存します。

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Context** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Context
    ```
    
1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注記**: ビルド エラーがある場合は、**すべてのファイル (F):\\Allfiles\\Labs\\03\\Solution\\AdventureWorks\\AdventureWorks.Context** フォルダにある **AdventureWorksCosmosContext.cs** ファイルを確認してください。

1.  [**ゴミ箱**] アイコンを選択して、現在開いている端子と関連するプロセスを破棄します。

#### タスク 3: Azure Cosmos DB 接続文字列の更新

1.  Visual Studio コード ペインの**エクスプローラー** ウインドウで、**AdventureWorks.Web** プロジェクトを展開します。

1.  **appsettings.json** ファイルをダブルクリック (またはダブル選択) します。

1.  JSON オブジェクトの4行目で **ConnectionStrings.AdventureWorksCosmosContext** パスを見つけます。現在値が空であることを確認します：

    ```
    "ConnectionStrings": {
        ...
        "AdventureWorksCosmosContext": "",
        ...
    },
    ```

1.  このラボで前に記録した**Azure Cosmos DB アカウント**の**一次接続文字列** に値を設定して、**AdventureWorksCosmosContext** プロパティの値を更新します。

1.  **appsettings.json**ファイルを保存します。

#### タスク 4: .NET アプリケーションのスタートアップ ロジックの更新

1.  Visual Studio コード ペインの**エクスプローラー** ウインドウで、**AdventureWorks.Web** プロジェクトを展開します。

1.  **Startup.cs** ファイルをダブルクリック (またはダブル選択) します。 

1.  **Startup** クラスで、既存の **ConfigureProductService** メソッドを見つけます。

    ```
    public void ConfigureProductService(IServiceCollection services)
    {
        services.AddScoped<IAdventureWorksProductContext, AdventureWorksSqlContext>(provider =>
            new AdventureWorksSqlContext(
                _configuration.GetConnectionString(nameof(AdventureWorksSqlContext))
            )
        );
    }
    ```

    > **注記**: 現在の製品サービスは、データベースとして SQL を使用します。

1.  **ConfigureProductService** メソッド内で、既存のすべてのコード行を削除します。

    ```
    public void ConfigureProductService(IServiceCollection services)
    {
    }
    ```

1.  **ConfigureProductService** メソッド内で、次のコードブロックを追加して、製品プロバイダーをこのラボで前に作成した **AdventureWorksCosmosContext** 実装に変更します。

    ```
    services.AddScoped<IAdventureWorksProductContext, AdventureWorksCosmosContext>(provider =>
        new AdventureWorksCosmosContext(
            _configuration.GetConnectionString(nameof(AdventureWorksCosmosContext))
        )
    );
    ```

1.  **Startup.cs** ファイルを保存します。

#### タスク 5: .NET アプリケーションが Azure Cosmos DB に正常に接続することを検証する

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Web** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Web\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注記**: ``dotnet run`` コマンドは、プロジェクトに対するすべての変更を自動的にビルドし、デバッガーをアタッチせずに Web アプリケーションを起動します。このコマンドは、実行中のアプリケーションの URL と割り当てられたポートを出力します。

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、現在実行中の Web アプリケーション (<http://localhost:5000>) に移動します。

1.  Web アプリケーションで、フロント ページに表示されるモデルの一覧を確認します。

1.  **Touring-1000** モデルを見 つけて、[**詳細の表示**] を選択します。

1.  **Touring-1000** 製品の詳細ページで、次の操作を実行します。

    1.  [**オプションの選択**] ボックスの一覧 で、[**Touring-1000 Yellow, 50, $2,384.07**]を選択します。   
    
    1.  [**カートに追加**] を選択します。

1.  チェックアウト機能が無効のままであることを確認します。

    > **注記**: 次の演習では、チェックアウト ロジックを実装します。

1.  Web アプリケーションを表示するブラウザー ウィンドウを閉じます。

1.  **Visual Studio Code** ウィンドウに戻ります。

1.  **Visual Studio Code** ウィンドウに戻り、 **ゴミ箱**アイコンを選択して、現在開いているターミナルと関連プロセスを破棄します。

#### 確認

この演習では、.NET SDK を使用して Azure Cosmos DB コレクションを照会する C# コードを作成しました。

### エクササイズ 6: NET を使用した Azure Cache for Redis へのアクセス

#### タスク 1: StackExchange.Redis SDK および参照を使用してライブラリを更新する

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Context** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Context\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NuGet から **Newtonsoft.Json** をインポートします。

    ```
    dotnet add package Newtonsoft.Json --version 12.0.2
    ```

    > **注記**: ``dotnet add package`` コマンドは、**NuGet** から **[Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/12.0.2)** パッケージを追加します。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NuGet から **StackExchange.Redis** をインポートします。

    ```
    dotnet add package StackExchange.Redis --version 2.0.601
    ```

    > **注記**: ``dotnet add package`` コマンド は、**NuGet** から **[StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/2.0.601)** パッケージを追加します。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  [**ゴミ箱**] アイコンを選択して、現在開いている端子と関連するプロセスを破棄します。

#### タスク 2: Azure Cache for Redis に接続する .NET コードを書き込みます。

1.  Visual Studio コード ペインの**エクスプローラー** ウインドウで、**AdventureWorks.Context** プロジェクトを展開します。

1.  コンテキストメニューにアクセスするか、 **AdventureWorks.Context** フォルダーノードを右クリックして、[**新しいファイル**] を選択します。

1.  表示されるプロンプトで、**AdventureWorksRedisContext.cs** の値を入力します。

1.  **AdventureWorksRedisContext.cs** ファイルのコード エディタ タブで、次のコード行を追加して、参照されている **AdventureWorks.Models** プロジェクトから **AdventureWorks.Models** 名前空間をインポートします。

    ```
    using AdventureWorks.Models;
    ```

1.  次のコード行を追加して、NuGetからインポートされた **Newtonsoft.Json** パッケージから **Newtonsoft.Json** 名前空間をインポートします。

    ```
    using Newtonsoft.Json;
    ```

1.  次のコード行を追加して、NuGetからインポートされた **StackExchange.Redis** パッケージから **StackExchange.Redis** 名前空間をインポートします。

    ```
    using StackExchange.Redis;
    ```

1.  次のコード行を追加して、このファイルで使用される組み込み名前空間の **using** ディレクティブを追加します。

    ```
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  次のコードを入力して、**AdventureWorks.Context** 名前空間ブロックを追加します。

    ```
    namespace AdventureWorks.Context
    {
    }
    ```

1.  **AdventureWorks.Context** 名前空間内で、次のコードを入力して、新しい **AdventureWorksRedisContext** クラスを作成します。

    ```
    public class AdventureWorksRedisContext
    {
    }
    ```

1.  このクラスが **IAdventureWorksCheckoutContext** インターフェイスを実装することを示す仕様を追加して、**AdventureWorksRedisContext** クラスの宣言を更新します。

    ```
    public class AdventureWorksRedisContext : IAdventureWorksCheckoutContext
    {
    }
    ```

1.  **AdventureWorksRedisContext** クラス内で、次のコード行を入力して、**_database** と名付けられた読み取り専用の新しい **IDatabase** 変数を作成します。

    ```
    private readonly IDatabase _database;
    ```

1.  **AdventureWorksRedisContext** クラス内で、次のシグネチャを持つ新しいコンストラクターを追加します。

    ```
    public AdventureWorksRedisContext(string connectionString)
    {        
    }
    ```

1.  コンストラクター内で、次のコード ブロックを追加して、**ConnectionMultiplexer** クラスの新しいインスタンスを作成し、データベース インスタンスを取得します。

    ```
    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect(connectionString);
    _database = connection.GetDatabase();
    ```

1.  **AdventureWorksRedisContext** クラス内で、次のシグネチャを持つ新しい **AddProductToCartAsync** メソッドを追加します。

    ```
    public async Task AddProductToCartAsync(string uniqueIdentifier, Product product)
    {        
    }
    ```

1.  **AddProductToCartAsync** メソッド内で、次のコード ブロックを追加してキーから現在の値を取得し、リストが存在しない場合は新しいリストを作成し、製品をリストに追加してから、データベースのキーの新しい値としてリストを保存します。
    
    ```
    RedisValue result = await _database.StringGetAsync(uniqueIdentifier);
    List<Product> products = new List<Product>();
    if (!result.IsNullOrEmpty)
    {
        List<Product> parsed = JsonConvert.DeserializeObject<List<Product>>(result.ToString());
        products.AddRange(parsed);
    }
    products.Add(product);
    string json = JsonConvert.SerializeObject(products);
    await _database.StringSetAsync(uniqueIdentifier, json);
    ```

1.  **AdventureWorksRedisContext** クラス内で、次のシグネチャを持つ新しい **GetProductsInCartAsync** メソッドを追加します。

    ```
    public async Task<List<Product>> GetProductsInCartAsync(string uniqueIdentifier)
    {        
    }
    ```

1.  **GetProductsInCartAsync** メソッド内で、以下のコード行を追加してデータベースからリストを取得し、JSON 値を **Product** インスタンスのコレクションに解析します。
    
    ```    
    string json = await _database.StringGetAsync(uniqueIdentifier);
    List<Product> products = JsonConvert.DeserializeObject<List<Product>>(json ?? "[]");
    return products;
    ```

1.  **AdventureWorksRedisContext** クラス内で、次のシグネチャを持つ新しい **ClearCart** メソッドを追加します。

    ```
    public async Task ClearCart(string uniqueIdentifier)
    {        
    }
    ```

1.  **ClearCart** メソッド内で、次のコード行を追加して、データベースからキーとその関連値を削除します。
    
    ```
    await _database.KeyDeleteAsync(uniqueIdentifier);
    ```

1.  **AdventureWorksRedisContext.cs** ファイルを保存します。

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Context** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Context
    ```
    
1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注記**: ビルド エラーがある場合は、**すべてのファイル (F):\\Allfiles\\Labs\\03\\Solution\\AdventureWorks\\AdventureWorks.Context** フォルダにある **AdventureWorksRedisContext.cs** ファイルを確認してください。

1.  [**ゴミ箱**] アイコンを選択して、現在開いている端子と関連するプロセスを破棄します。

#### タスク 3: Redis 接続文字列の更新

1.  Visual Studio コード ペインの**エクスプローラー** ウインドウで、**AdventureWorks.Web** プロジェクトを展開します。

1.  **appsettings.json** ファイルをダブルクリック (またはダブル選択) します。

1.  JSON オブジェクトの4行目で **ConnectionStrings.AdventureWorksRedisContext** パスを見つけます。現在値が空であることを確認します：

    ```
    "ConnectionStrings": {
        ...
        "AdventureWorksRedisContext": ""
    },
    ```

1.  **AdventureWorksRedisContext** プロパティの値を更新するには、このラボで以前に記録した **Azure Cache for Redis** インスタンスの**一次接続文字列 (StackExchange.Redis)** に値を設定します。

1.  JSON オブジェクトの9行目で、**Settings.CartAvailable** パスを見つけます。現在値が **false** であることを確認します：

    ```
    "Settings": {
        ...
        "CartAvailable": false,
        ...
    }
    ```

1.  値を **true** に設定して、**CartAvailable** プロパティの値を更新します。

    ```
    "CartAvailable": true,
    ```

1.  **appsettings.json**ファイルを保存します。

#### タスク 4: .NET アプリケーションのスタートアップ ロジックの更新

1.  Visual Studio コード ペインの**エクスプローラー** ウインドウで、**AdventureWorks.Web** プロジェクトを展開します。

1.  **Startup.cs** ファイルをダブルクリック (またはダブル選択) します。

1.  **Startup** クラスで、既存の **ConfigureCheckoutService** メソッドを見つけます。

    ```
    public void ConfigureCheckoutService(IServiceCollection services)
    {
        services.AddScoped<IAdventureWorksCheckoutContext>(provider =>
            new Mock<IAdventureWorksCheckoutContext>().Object
        );
    }
    ```

    > **注記**: 現在のチェックアウト サービスは、データベースとしてモックを使用します。

1.  **ConfigureCheckoutService** メソッド内で、既存のすべてのコード行を削除します。

    ```
    public void ConfigureCheckoutService(IServiceCollection services)
    {
    }
    ```

1.  **ConfigureCheckoutService** メソッド内で、次のコードブロックを追加して、チェックアウト プロバイダーをこのラボで前に作成した **AdventureWorksRedisContext** 実装に変更します。

    ```
    services.AddScoped<IAdventureWorksCheckoutContext, AdventureWorksRedisContext>(provider =>
        new AdventureWorksRedisContext(
            _configuration.GetConnectionString(nameof(AdventureWorksRedisContext))
        )
    );
    ```

1.  **Startup.cs** ファイルを保存します。

#### タスク 5: .NET アプリケーションが Azure Cache for Redis に正常に接続することを検証する

1.  Visual Studio コード ウインドウで、コンテキスト メニューにアクセスするか、**エクスプローラ**ペインを右クリックし、**ターミナルで開く**を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Web** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Web\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NET Core Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注記**: ``dotnet run`` コマンドは、プロジェクトに対するすべての変更を自動的にビルドし、デバッガーをアタッチせずに Web アプリケーションを起動します。このコマンドは、実行中のアプリケーションの URL と割り当てられたポートを出力します。

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、現在実行中の Web アプリケーション (<http://localhost:5000>) に移動します。

1.  Web アプリケーションで、フロント ページに表示されるモデルの一覧を確認します。

1.  **Mountain-400-W** モデルを見つけて、[**詳細の表示**] を選択します。   

1.  **Mountain-400-W** 製品の詳細ページで、次の操作を実行します。

    1.  [**オプションの選択**] ボックスの一覧 で、[**Mountain-400-W Silver, 40, $769.49**]を選択します。
    
    1.  [**カートに追加**] を選択します。

1.  ショッピング カート ページで、カートの内容を確認し、[**チェックアウト**] を選択します。 

1.  チェックアウト ページで、最終的な領収書を確認します。

1.  ページ上部の**ショッピング カート**アイコンを選択します。

1.  ショッピング カート ページで、空のカートを確認します。

1.  Web アプリケーションを表示するブラウザー ウィンドウを閉じます。

1.  **Visual Studio Code** ウィンドウに戻り、 **ゴミ箱**アイコンを選択して、現在開いているターミナルと関連プロセスを破棄します。

#### 確認

この演習では、C# コードを使用して、Azure Cache for Redis ストアからデータを格納および取得しました。

### エクササイズ 7: サブスクリプションのクリーンアップ 

#### タスク 1: Azure Cloud Shell を開く

1.  ポータルの上部で、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。

    > **注記**：**Cloud Shell** アイコンは、シンボルとアンダースコア文字より大きい文字で表されます。

1.  サブスクリプションを使用して初めて **Cloud Shell** を開く場合は、初めて使用する **Cloud Shell** を構成できる**Azure Cloud シェルへようこそウィザード**が表示されます。ウィザードで次の操作を実行します。
    
    1.  ダイアログボックスを表示すると、シェルを使用して開始する新しいストレージ アカウントを作成するよう求めるメッセージが表示されます。既定の設定を受け入れ、**ストレージの作成**を選択します。
    
    1.  **Cloud Shell** が初回のセットアップ手順を完了するのを待ってから、ラボを進めます。

    > **注記**: **Cloud Shell** の構成オプションが表示されない場合は、このコースの演習で既存のサブスクリプションを使用している可能性が高いと考えられます。演習は、新しいサブスクリプションを使用しているという推定から記述されます。

1.  ポータルの下部にある **Cloud Shell** コマンド プロンプトで次のコマンドを入力し、Enterキーを押してサブスクリプション内のすべてのリソース グループを一覧表示します。

    ```
    az group list
    ```
1.  プロンプトで次のコマンドを入力し、Enter キーを押して、リソース グループを削除する可能性のあるコマンドの一覧を表示します。

    ```
    az group delete --help
    ```

#### タスク 2: リソース グループを削除する

1.  プロンプトで次のコマンドを入力し、Enter キーを押して **PolyglotData** リソース グループを削除します。

    ```
    az group delete --name PolyglotData --no-wait --yes
    ```
    
1.  ポータルの下部にある **Cloud Shell** ペインを閉じます。

#### タスク 3: アクティブなアプリケーションを閉じる

1.  現在実行中の **Microsoft Edge** アプリケーションを閉じます。

1.  現在実行中の **Visual Studio Code** アプリケーションを閉じます。

#### 復習

この実習では、この演習で使用する **リソース グループ** を削除してサブスクリプションをクリーンアップしました。
