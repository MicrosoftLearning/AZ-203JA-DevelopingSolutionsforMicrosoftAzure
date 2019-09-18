---
lab:
    title: 'ラボ: サービス間でリソースシークレットに安全にアクセスする'
    type: 'Answer Key'
    module: 'モジュール 4：Azure Security の実装'
---

# ラボ: サービス間でリソース シークレットに安全にアクセスする
# 受講ラボの解答キー

## Microsoft Azure ユーザー インターフェイス

Microsoft クラウド ツールのダイナミックな性質を考えると、このトレーニング コンテンツの開発後に Azure ユーザー インターフェイス (UI) の変更が発生する可能性があります。これらの変更により、演習の手順と演習手順が一致しない場合があります。

Microsoft は、コミュニティが必要な変更を行うとすぐに、このトレーニング コースを更新します。しかし、クラウド更新が頻繁に起きるため、この研修内容が更新される前に、UI の変更を経験するかも知れません。 **その場合は変更に順応して、必要に応じてラボでをそれを処理してください。**

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

### エクササイズ 1: Azureのリソースを作成

#### タスク 1: Azure portalを開く

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

2.  開いているブラウザ ウインドウで、**Azure portal** ([portal.azure.com](https://portal.azure.com))に移動します。

3.  Microsoft アカウントの **電子メール アドレス** を入力します。

4.  **次へ** を選択します。

5.  Microsoft アカウントの **パスワード** を入力します。

6.  **サインイン** を選択します。

> > 注記：**Azure portal** に初めてサインインする場合は、ポータルのツアーを提供するダイアログ ボックスが表示されます。ツアーをスキップしてポータルの使用を開始するには、**開始** を選択します。

#### タスク 2: Azure Storage  アカウントを作成する

1.  Azure portalの左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーションペインをクリックしてください。

2.  **すべてのサービス** ブレードで、**ストレージ アカウント** を選択します。

3.  **ストレージ アカウント** ブレードで、ストレージ インスタンスの一覧を表示します。

4.  **ストレージ アカウント** ブレードの上部にある **追加** を選択 します。

5.  **ストレージ アカウント作成** ブレードで、**基本** などのブレードの上部にあるタブを確認します。

> 注記：各タブは、ワークフロー内の新しい **ストレージ アカウント** を作成するためのステップを表 します。 いつでも **レビュー + 作成** を選択して、残りのタブをスキップできます。

6.  **基本** タブで、次の操作を実行します：
    
    1.  **サブスクリプション** テキスト ボックスは既定値のままにします。
    
    2.  **リソース グループ** セクションで、**新規作成** を選択し、**SecureFunction** を選択し、**OK** を選択します。
    
    3.  **ストレージ アカウント** **名** テキスト ボックスに、**securestor\[名前を小文字で入力\]** と入力します。
    
    4.  **場所** ドロップダウン リストで、 **米国東部** リージョンを選択します。
    
    5.  **パフォーマンス** セクションで、**標準** を選択します。
    
    6.  **アカウントの種類** ドロップダウン リストで、**StorageV2 (汎用 v2)** を選択します。
    
    7.  **レプリケーション** ドロップダウン リストで、**ローカル冗長ストレージ (LRS)** を選択します。
    
    8.  **アクセス層** セクションで、**Hot ** が選択されていることを確認します。
    
    9.  **レビュー + 作成** を選択します。

7.  **レビュー + 作成** タブで、前の手順で選択したオプションを確認します。

8.  指定した構成を使用してストレージ アカウントを作成するには、**作成** を選択します。

9.  演習を進める前に、作成タスクが完了するまで待ちます。

10. Azureポータルの左側にあるナビゲーションペインで、**すべてのサービス** ナビゲーションペインをクリックしてください。

11. **すべてのサービス** ブレードで、**ストレージ アカウント** を選択します。

12. **ストレージ アカウント** ブレードで、プレフィックス **セキュアスタを** 持つストレージ アカウント インスタンスを選択します。 

13. **ストレージ アカウント** ブレードで、ブレードの左側にある **設定** セクションを見つけ、**アクセスキー** リンクを選択 します。

14. **アクセス キー** ブレードでいずれかのキーを選択し、 **接続文字列** テキスト ボックスに値を記録します。これらの値は、この演習の後半で使用します。

> > 注記：使用を選択する接続文字列は関係ありません。それらは交換可能です。

#### タスク 3: Azure Key Vault を作成します。

1.  ポータルの左側にあるナビゲーション メニューで、**+ リソースを作成** リンクを選択します。

2.  **新しい** ブレードの上部で、 おすすめサービスの一覧の上にある **マーケットプレースの検索** テキスト ボックスを検索します。

3.  検索テキスト ボックスに **ボルト** を入力し、Enterを押します。

4.  **すべて** 検索結果 ブレードで、**キー ボルト** の結果を選択します。

5.  **キー ボルト** ブレードで、 **作成** を選択します。

6.  **キー ボルトの作成** ブレードで、次の操作を実行します。
    
    1.  **名前** テキストボックスに **securevault\[*名前を小文字*\]** と入力します。
    
    2.  **サブスクリプション** テキスト ボックスは既定値のままにします。
    
    3.  **リソース グループ** セクションで、 **既存のものを使用** を選択し、**SecureFunction** を選択します。
    
    4.  **場所** ドロップダウン リストで、**米国東部** を選択します。
    
    5.  **価格層** テキスト ボックスは、既定値のままにします。
    
    6.  **アクセス ポリシー** テキスト ボックスは既定値のままにします。 
    
    7.  **仮想ネットワーク アクセス** テキスト ボックスを既定値のままにします。 
    
    8.  **作成** を選択します。

7.  演習を進める前に、作成タスクが完了するまで待ちます。

#### タスク 4: Azure Functionアプリの作成

1.  ポータルの左側にあるナビゲーション メニューで、**+ リソースを作成** リンクを選択します。

2.  **新しい** ブレードの上部で、 おすすめサービスの一覧の上にある **マーケットプレースの検索** テキスト ボックスを検索します。

3.  検索テキスト ボックスに **関数** を入力し、Enterを押します。

4.  **すべて** 検索結果ブレードで、 **関数アプリ** の結果を選択します。

5.  **関数アプリ** ブレードで、**作成** を選択します。

6.  **関数アプリの作成** ブレードで、次の操作を実行します。
    
    1.  **アプリ名** テキストボックスに **securevault\[*名前を小文字*\]** と入力します。
    
    2.  **サブスクリプション** テキスト ボックスは既定値のままにします。
    
    3.  **リソース グループ** セクションで、**既存のものを使用** を選択し、**SecureFunction** を選択します。
    
    4.  **OS** セクションで、**Windows** を選択 します。   
    
    5.  **ホスティング プラン** ドロップダウン リストで、**消費プラン** を選択します。
    
    6.  **場所** ドロップダウン リストで、**米国東部** を選択します。
    
    7.  **ランタイム スタック** ドロップダウン リストで、**.NET** を選択します。
    
    8.  **ストレージ** セクションで **既存のものを使用** を選択し、一覧から **securestor\[小文字で名前]** を選択します。   
    
    9.  **アプリケーション インサイト** テキスト ボックスは既定値のままにします。 
    
    10. **作成** を選択します。

7.  演習を進める前に、作成タスクが完了するまで待ちます。

#### 復習

この演習では、この演習で使用するすべてのリソースを作成しました。

### エクササイズ 2: シークレットと ID の構成 

#### タスク 1: システムに割り当てられた管理サービス ID の構成

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ** リンクを選択します。

2.  **リソース グループ** ブレードで、 この演習で前に作成した **SecureFunction** リソース グループを見つけて選択します。

3.  **SecureFunction** ブレードで、このラボで前に作成した **securefunc\*** 関数アプリを選択します。  

4.  **機能アプリ** ブレードで、 **プラットフォームの機能** タブを選択します。

5.  **プラットフォームの機能** タブで、 **ネットワーク** セクションにある **ID** リンクを選択 します。     

6.  **ID** ブレードで、**システムに割り当てられた** タブを見つけて、次のアクションを実行します。   
    
    1.  **ステータス**セクションで、**オン**を選択します。 
    
    2.  **保存** を選択します。
    
    3.  確認ダイアログで **はい** を選択します。

7.  この演習を進める前に、システムに割り当てられた管理 ID が作成されるまで待ちます。

#### タスク 2: Key Vaultを作成します

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ** リンクを選択します。

2.  **リソース グループ** ブレードで、 この演習で前に作成した **SecureFunction** リソース グループを見つけて選択します。

3.  **SecureFunction** ブレードで、この演習で前に作成した **securevault\*** キー ボルトを選択します。

4.  **キー ボルト** タブで、**設定** セクションにある **シークレット** リンクを選択 します。

5.  **シークレット** ペインで、 **生成/インポート** を選択します。   

6.  **シークレットの作成** ブレードで、次の操作を実行します。
    
    1.  **アップロード オプションの** ドロップダウン リストで、 **手動** を選択します。
    
    2.  **名前** テキスト ボックスに、**ストレージ資格情報** を入力します。
    
    3.  **値** テキスト ボックスに、この演習で前に記録したストレージ アカウント **接続文字列を** 入力します。  
    
    4.  **内容種別** テキスト ボックスは既定値のままにします。
    
    5.  **設定の開始日** テキスト ボックスは既定値のままにします。 
    
    6.  **有効期限の設定** テキスト ボックスは既定値のままにします。 
    
    7.  **有効** セクションで、**はい** を選択します。   
    
    8.  **作成** を選択します。

7.  この演習を進める前に、シークレットが作成されるのを待ちます。

8.  **シークレット** ウインドウに戻り、リスト内の **ストレージ資格情報** 項目を選択します。

9.  **バージョン** ウインドウで、**ストレージ資格情報**シークレットの最新バージョンを選択します。

10. **シークレット バージョン** ウインドウで、次の操作を実行します。
    
    9.  シークレットの最新バージョンのメタデータを確認します。
    
    10. シークレットの値を表示するには、**シークレット値を表示** を選択します。
    
    11. これを後の演習で使用するため、**シークレット識別子** テキスト ボックスの値を記録します。

> > 注記：**シークレット値** フィールドではなく、 **シークレット識別子** フィールドの値を記録しています。   

#### タスク 3: キー ボルト アクセス ポリシーの構成

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ** リンクを選択します。

2.  **リソース グループ** ブレードで、 この演習で前に作成した **SecureFunction** リソース グループを見つけて選択します。

3.  **SecureFunction** ブレードで、この演習で前に作成した **securevault\*** キー ボルトを選択します。

4.  **キー ボルト** タブで、**設定** セクションにある **アクセス ポリシー** リンクを選択 します。

5.  **アクセス ポリシー** ペインで、**新規追加** を選択します。 

6.  **アクセス ポリシーの追加** ブレードで、次の操作を実行します。 
    
    1.  **プリンシパルの選択** リンクを選択します。 
    
    2.  **プリンシパル** ブレードで、**securefunc\[名前を小文字で指定]** という名前のサービス プリンシパルを見つけて選択し、**選択** を選択します。
    
    3.  **キーアクセス許可** リストは既定値に設定したままにします。 
    
    4.  シークレットアクセス許可ドロップダウン リストで、GET アクセス許可を選択します。
    
    5.  **証明書のアクセス許可** リストは、既定値に設定したままにします。 
    
    6.  **承認済みアプリケーション** テキスト ボックスは、既定値のままにしておきます。 
    
    7.  **OK** を選択します。

7.  **アクセス ポリシー** ペインに戻る場合は、**保存** を選択します。

8.  この演習を進める前に、アクセス ポリシーに対する変更が保存されるのを待ちます。

#### 復習

この演習では、関数アプリにサーバー割り当てが行われた管理サービス ID を作成し、Key Vault でシークレットの値を取得するための適切なアクセス許可をその ID に付与しました。最後に、関数アプリ内で使用するシークレットを作成しました。

### エクササイズ 3: 関数アプリ コードの作成 

#### タスク 1: キー ボルト派生アプリケーション設定を作成する 

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ** リンクを選択します。

2.  **リソース グループ** ブレードで、 この演習で前に作成した **SecureFunction** リソース グループを見つけて選択します。

3.  **SecureFunction** ブレードで、このラボで前に作成した **securefunc\*** 関数アプリを選択します。

4.  **機能アプリ** ブレードで、**プラットフォームの機能** タブを選択します。

5.  **プラットフォームの機能** タブで、**一般設定** セクションにある **アプリケーション設定** リンクを選択 します。

6.  **アプリケーション設定** タブで、次の操作を実行します：
    
    1.  **アプリケーション設定** セクションが表示されるまで、下にスクロールします。
    
    2.  **新しい出席者の追加** を選択します。
    
    3.  **名前を入力** テキストボックスに、**StorageConnectionString** を入力します。
    
    4.  **値を入力** ボックスで、次の構文を使用して値を作成します。 **@Microsoft.KeyVault(SecretUri=\<Secret Identifier\>)**

> > 注記：上記の構文を使用して、**シークレット識別子** への参照を構築する必要があります。たとえば、シークレット識別子 **がhttps://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf**の場合、値は **@Microsoft.KeyVault(SecretUri= https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf)** になります。

5.  **スロット設定** テキスト ボックスは、既定値のままにしておきます。

6.  タブの上部まで戻り、**保存** を選択します。

<!-- end list -->

7.  演習を進める前に、アプリケーションの設定が保持されるまで待ちます。

#### タスク 2: HTTP トリガ関数の作成

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ** リンクを選択します。

2.  **リソース グループ** ブレードで、 この演習で前に作成した **SecureFunction** リソース グループを見つけて選択します。

3.  **SecureFunction** ブレードで、このラボで前に作成した **securefunc\*** 関数アプリを選択します。

4.  **機能アプリ** ブレードで、 **+ 新機能** を選択します。

5.  **新しい Azure Function** のクイック スタートで、次のアクションを実行します。
    
    1.  **開発環境の選択** ヘッダーで、**ポータル内** を選択します。
    
    2.  **続行** を選択します。
    
    3.  **関数の選択** ヘッダーで、**その他のテンプレート** を選択します。
    
    4.  **テンプレートの終了と表示** を選択します。
    
    5.  **テンプレート** ドロップダウン リストで、**HTTPトリガ** を選択します。
    
    6.  **新機能** ポップアップで **名前** テキスト ボックスを検索し、**FileParser** を入力します。
    
    7.  **新機能** ポップアップで、**承認レベル** リストを検索し、**匿名** を選択します。
    
    8.  **新機能** ポップアップで、**作成** を選択します。   

6.  関数エディタで、関数スクリプトの例を確認します。

\#r "Newtonsoft.Json"

using System.Net;

using Microsoft.AspNetCore.Mvc;

using Microsoft.Extensions.Primitives;

using Newtonsoft.Json;

public static async Task\<IActionResult\> Run(HttpRequest req, ILogger log)

{

log.LogInformation("C\# HTTP trigger function processed a request.");

string name = req.Query\["name"\];

string requestBody = await new StreamReader(req.Body).ReadToEndAsync();

dynamic data = JsonConvert.DeserializeObject(requestBody);

name = name ?? data?.name;

return name \!= null

? (ActionResult)new OkObjectResult($"Hello, {name}")

: new BadRequestObjectResult("Please pass a name on the query string or in the request body");

}

7.  サンプル コードをすべて **削除** します。

8.  関数エディタ内で、次のプレースホルダ関数をコピーして貼り付けます。

using System.Net;

using Microsoft.AspNetCore.Mvc;

public static async Task\<IActionResult\> Run(HttpRequest req)

{

return new OkObjectResult("Test Successful");

}

9.  **保存して実行** を選択してスクリプトを保存し、関数のテスト実行を実行します。 

10. スクリプトが初めて実行されると、**テスト** ペインと **ログ** ペインが自動的に表示されます。   

11. **テスト** ウインドウの **出力** ボックスに従います。これで、関数から返される **テスト成功** の値が表示されます。

#### タスク 3: アプリケーション設定のテスト

1.  スクリプトの **Run** メソッド内の既存のコードを削除します。

2.  **Run** メソッドは次のようになります: 

using System.Net;

using Microsoft.AspNetCore.Mvc;

public static async Task\<IActionResult\> Run(HttpRequest req)

{

}

3.  次のコード行を追加して、**Environment.GetEnvironmentVariable** メソッドを使用して、 **StorageConnectionString** アプリケーション設定の値を取得します。

string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");

4.  次のコード行を追加して、 **OkObjectResult** クラス コンストラクタを使用することで、 **connectionString** 変数の値を返します:

return new OkObjectResult(connectionString);

5.  **Run** メソッドは次のようになります:

using System.Net;

using Microsoft.AspNetCore.Mvc;

public static async Task\<IActionResult\> Run(HttpRequest req)

{

string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");

return new OkObjectResult(connectionString);

}

6.  **保存して実行** を選択してスクリプトを保存し、関数のテスト実行を実行します。

7.  **テスト** ウインドウの **出力** ボックスに従います。これで、関数から返される接続文字列が表示されます。

#### 復習

この演習では、サービス ID を安全に使用して、**Azure Key Vault** に格納されているシークレットの値を読み取り、**Azure Function** の結果としてその値を返 します。

### エクササイズ 4: ストレージ アカウントの BLOB にアクセス

#### タスク 1: サンプルストレージ BLOB のアップロード

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ** リンクを選択します。

2.  **リソース グループ** ブレードで、 この演習で前に作成した **SecureFunction** リソース グループを見つけて選択します。

3.  **SecureFunction** ブレードで、 この実習ラボで前に作成した **securestor\*** ストレージ アカウントを選択します。

4.  **ストレージ アカウント** ブレードで、ブレードの左側にある **BLOB サービス** セクションにある **BLOB** リンクを選択します。 

5.  **BLOB** セクションで、 **+ コンテナ** を選択します。

6.  **新規コンテナ** ポップアップで、次の操作を実行します。
    
    1.  **名前** テキスト ボックスに、**drop** を入力します。 
    
    2.  **パブリック アクセス レベル** ドロップダウン リストで、**BLOB (BLOBのみの匿名読み取りアクセス)** を選択します。
    
    3.  **OK** を選択します。

7.  **BLOB** セクションに戻 り、新しく作成した **ドロップ** コンテナを選択します。

8.  **コンテナ** ブレードで、**アップロード** を選択します。   

9.  **BLOB をアップロード** ポップアップで、次の操作を実行します。
    
    4.  **ファイル** セクションで、**フォルダ** アイコンを選択します。   
    
    5.  ファイル エクスプローラ ダイアログ ボックスで、**すべてのファイル (F):Labfiles\\04\\Starter** に移動し、**records.json** ファイルを選択し、**開く** を選択します。
    
    6.  **ファイルが既に存在する場合は、上書き** が選択されていることを確認します。 
    
    7.  **アップロード** を選択します。

10. この演習を続行する前に、BLOBがアップロードされるのを待ちます。

11. **コンテナ** ブレードに戻 り、BLOBの一覧から **records.json** BLOB を選択します。  

12. **BLOB** ブレードで、BLOBメタデータを表示します。 

13. BLOBの **URL** をコピーします。

14. タスク バーで、**Microsoft Edge** アイコンを右に選択し、**新しいウインドウ** を選択します。

15. 新しいブラウザ ウインドウで、BLOB用にコピーした **URL** に移動します。

16. これで、BLOB の **JSON** コンテンツが表示されます。 **JSON** の内容を示すブラウザ ウインドウを閉じます。

17. **Azure portal** を使用してブラウザ ウインドウに戻 ります。

18. **BLOB** ブレードを閉じます。

19. **コンテナ** ブレードに戻り、 ブレードの上部にある **アクセス レベル ポリシーの変更** を選択します。 

20. 表示される **アクセス レベルの変更** ポップアップで、次のアクションを実行します。 
    
    8.  **パブリック アクセス レベル** ドロップダウン リストで、 **プライベート(匿名アクセスなし)** を選択します。
    
    9.  **OK** を選択します。

21. タスク バーで、**Microsoft Edge** アイコンを右に選択し、**新しいウインドウ** を選択します。

22. 新しいブラウザ ウインドウで、BLOB 用にコピーした **URL** に移動します。

23. リソースが見つからなかったことを示すエラー メッセージが表示されます。

> > 注記：エラー メッセージが表示されない場合は、ブラウザがファイルをキャッシュしている可能性があります。エラー メッセージが表示されるまで、**Ctrl + F5** を使用してページを更新します。 

#### タスク 2: Storage アカウント SDK の構成

1.  ポータルの左側にあるナビゲーション メニューで、**リソース グループ** リンクを選択します。

2.  **リソース グループ** ブレードで、 この演習で前に作成した **SecureFunction** リソース グループを見つけて選択します。

3.  **SecureFunction** ブレードで、このラボで前に作成した **securefunc\*** 関数アプリを選択します。

4.  **関数アプリ** ブレードで、既存の **FileParser** 関数を見つけて選択して、関数のエディタを開きます。   

> > 注記：ブレードの左側にあるメニューで **機能** オプションを展開する必要がある場合があります。

5.  エディタの右側で、**ファイルの表示** を選択してタブを開きます。 

6.  **ファイルの表示** タブで、**アップロード** を選択します。   

7.  開くファイル エクスプローラ ダイアログ ボックスで、**すべてのファイル (F):Labfiles\\04\\Starter** に移動 し、**function.proj** ファイルを選択 し、**開く** を選択します。

8.  ファイルの内容を表示するには、**function.proj** ファイルを選択します。

9.  **FileParser** 関数のエディタに戻る **run.csx** ファイルを選択します。

10. **ファイルの表示** タブを最小化します。 

> > 注記：タブ ヘッダーのすぐ右にある矢印を選択して、タブを最小化できます。

11. エディタ内で、スクリプトの **Run** メソッド内の既存のコードを削除します。 

12. コード ファイルの上部に、次のコード行を追加して、**Microsoft.WindowsAzure.Storage** 名前空間の **using ブロック** を作成します。 

using Microsoft.WindowsAzure.Storage;

13. **Microsoft.WindowsAzure.Storage.Blob** 名前空間の **using ブロック** を作成するには、次のコード行を追加します。

using Microsoft.WindowsAzure.Storage.Blob;

14. **Run** メソッドは次のようになります:

using System.Net;

using Microsoft.AspNetCore.Mvc;

using Microsoft.WindowsAzure.Storage;

using Microsoft.WindowsAzure.Storage.Blob;

public static async Task\<IActionResult\> Run(HttpRequest req)

{

}

#### タスク 3: ストレージ アカウント コードの書き込み

1.  **Environment.GetEnvironmentVariable** メソッドを使用して **StorageConnectionString** アプリケーション設定の値を取得するには、**Run** メソッド内に次のコード行を追加します。

string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");

2.  次のコード行を追加 して、**CloudStorageAccount.Parse** 静的メソッドを使用して **CloudStorageAccount** クラスの新しいインスタンスを作成 し、*connectionString* 変数を渡します。   

CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

3.  **CloudStorageAccount.CreateCloudBlobClient メソッド** を使用して、ストレージ アカウントの BLOB にアクセスできる **CloudBlobClient** クラスの新しいインスタンスを作成するには、次のコード行を追加します。

CloudBlobClient blobClient = account.CreateCloudBlobClient();

4.  **CloudBlobClient.GetContainerReference** メソッドを使用する次のコード行を追加し、**ドロップ** コンテナ名を渡して、この実習ラボで作成済みのコンテナを参照する **CloudBlobContainer** クラスの新しいインスタンスを作成します:     

CloudBlobContainer container = blobClient.GetContainerReference("drop");

5.  **CloudBlobClient.GetContainerReference** メソッドを使用する次のコード行を追加し、**ecords.json** BLOB名を渡して、この実習ラボでアップロード済みのBLOBを参照する **CloudBlockBlob** クラスの新しいインスタンスを作成します:

CloudBlockBlob blob = container.GetBlockBlobReference("records.json");

6.  **Run** メソッドは次のようになります:

using System.Net;

using Microsoft.AspNetCore.Mvc;

using Microsoft.WindowsAzure.Storage;

using Microsoft.WindowsAzure.Storage.Blob;

public static async Task\<IActionResult\> Run(HttpRequest req)

{

string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");

CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudBlobClient blobClient = account.CreateCloudBlobClient();

CloudBlobContainer container = blobClient.GetContainerReference("drop");

CloudBlockBlob blob = container.GetBlockBlobReference("records.json");

}

#### タスク 4: BLOB のダウンロード

1.  **CloudBlockBlob.DownloadTextAsync** メソッドを使用して、 参照される BLOB の内容を非同期にダウンロードし、その結果を *コンテンツ*という文字列変数に格納するには、次のコード行を追加します。

string content = await blob.DownloadTextAsync();

2.  次のコード行を追加して、**OkObjectResult** クラス コンストラクタを使用することで、 *content* 変数の値を返します:

return new OkObjectResult(content);

3.  **Run** メソッドは次のようになります:

using System.Net;

using Microsoft.AspNetCore.Mvc;

using Microsoft.WindowsAzure.Storage;

using Microsoft.WindowsAzure.Storage.Blob;

public static async Task\<IActionResult\> Run(HttpRequest req)

{

string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");

CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudBlobClient blobClient = account.CreateCloudBlobClient();

CloudBlobContainer container = blobClient.GetContainerReference("drop");

CloudBlockBlob blob = container.GetBlockBlobReference("records.json");

string content = await blob.DownloadTextAsync();

return new OkObjectResult(content);

}

4.  **保存して実行** を選択してスクリプトを保存し、関数のテスト実行を実行します。

5.  **テスト** ウインドウの **出力** ボックスに従います。これで、**ストレージ アカウント** に保存されている **$/drop/records.json** BLOBの内容が表示されます。

#### タスク 5: 共有アクセス署名(SAS)

1.  次のコードの行を **削除** します。

string content = await blob.DownloadTextAsync();

return new OkObjectResult(content);

2.  **Run** メソッドは次のようになります:

using System.Net;

using Microsoft.AspNetCore.Mvc;

using Microsoft.WindowsAzure.Storage;

using Microsoft.WindowsAzure.Storage.Blob;

public static async Task\<IActionResult\> Run(HttpRequest req)

{

string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");

CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudBlobClient blobClient = account.CreateCloudBlobClient();

CloudBlobContainer container = blobClient.GetContainerReference("drop");

CloudBlockBlob blob = container.GetBlockBlobReference("records.json");

}

3.  次の設定を使用して **SharedAccessPolicy** クラスの新しいインスタンスを作成するには、次のコード行を追加します。
    
      - **アクセス許可**: 読み取り:
    
      - **サービス範囲**: ブロブ
    
      - **リソースの種類**: オブジェクト
    
      - **有効期限:** 2時間
    
      - **Protocol(プロトコル):** HTTPS のみ

SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()

{

Permissions = SharedAccessAccountPermissions.Read,

Services = SharedAccessAccountServices.Blob,

ResourceTypes = SharedAccessAccountResourceTypes.Object,

SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),

Protocols = SharedAccessProtocol.HttpsOnly

};

4.  以下のコード行を追加して **CloudStorageAccount.GetSharedAcessSignature** メソッドを用いて、提供されたポリシーを使用することで新しい **共有アクセスシグネチャ(SAS)トークン** を作成し、*sasToken* という名前の文字列変数に結果を格納します:

string sasToken = account.GetSharedAccessSignature(policy);

5.  以下のコード列を追加して **CloudBlockBlob.Uri** プロパティと *sasToken* 文字列変数の値を連結し、その結果を*secureBlobUrl* という名前の新しい変数に格納します。

string secureBlobUrl = $"{blob.Uri}{sasToken}";

6.  次のコード行を追加して、**OkObjectResult** クラス コンストラクタを使用して*secureBlobUrl * 変数の値を返します。

return new OkObjectResult(secureBlobUrl);

7.  **Run** メソッドは次のようになります:

using System.Net;

using Microsoft.AspNetCore.Mvc;

using Microsoft.WindowsAzure.Storage;

using Microsoft.WindowsAzure.Storage.Blob;

public static async Task\<IActionResult\> Run(HttpRequest req)

{

string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");

CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudBlobClient blobClient = account.CreateCloudBlobClient();

CloudBlobContainer container = blobClient.GetContainerReference("drop");

CloudBlockBlob blob = container.GetBlockBlobReference("records.json");

SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()

{

Permissions = SharedAccessAccountPermissions.Read,

Services = SharedAccessAccountServices.Blob,

ResourceTypes = SharedAccessAccountResourceTypes.Object,

SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),

Protocols = SharedAccessProtocol.HttpsOnly

};

string sasToken = account.GetSharedAccessSignature(policy);

string secureBlobUrl = $"{blob.Uri}{sasToken}";

return new OkObjectResult(secureBlobUrl);

}

8.  **保存して実行** を選択してスクリプトを保存し、関数のテスト実行を実行します。

9.  **テスト** ウインドウの **出力** ボックスに従います。これで、セキュリティで保護されたBLOBへのアクセスに使用できる一意の **セキュリティで保護された URL** が表示されます。この **URL** は、この演習の次の手順で使用する必要があるため、記録します。

10. タスク バーで、**Microsoft Edge** アイコンを右に選択し、**新しいウインドウ** を選択します。

11. 新しいブラウザ ウインドウで、BLOB用にコピーした **セキュリティで保護された** **URL** に移動します。

12. これで、BLOBの **JSON** コンテンツが表示されます。 **JSON** の内容を示すブラウザ ウインドウを閉じます。

13. **Azure portal** を使用してブラウザ ウインドウに戻 ります。

#### 復習

この演習では、C\# コードを使用してストレージ アカウントに安全にアクセスし、BLOB の内容をダウンロードしてから、別のクライアントで BLOB に安全にアクセスするために使用できる SAS トークンを生成します。

### エクササイズ 5: サブスクリプションのクリーンアップ 

#### タスク 1: Azure Cloud Shellを開き、リソース グループを一覧表示する

1.  Azure portalの上部ナビゲーション バーで、**Cloud Shell** アイコンを選択 して新しいシェル インスタンスを開きます。 

2.  ポータルの下部にある**Cloud Shell** コマンド プロンプトで次のコマンドを入力し、Enterキーを押してサブスクリプション内のすべてのリソース グループを一覧表示します。

az group list

3.  プロンプトで次のコマンドを入力し、Enterキーを押して、リソース グループを削除する可能性のあるコマンドの一覧を表示します。

az group delete --help

#### タスク 2: リソース グループの削除

1.  プロンプトで次のコマンドを入力し、Enterキーを押して **SecureFunction** リソース グループを削除します。

az group delete --name SecureFunction --no-wait --yes

2.  ポータルの下部にある **Cloud Shell** ペインを閉じます。 

#### タスク 3: アクティブなアプリケーションを閉じる

> 現在実行中の **Microsoft Edge** アプリケーションを閉じます。

#### 復習

この実習では、この演習で使用する **リソース グループ** を削除してサブスクリプションをクリーンアップしました。
