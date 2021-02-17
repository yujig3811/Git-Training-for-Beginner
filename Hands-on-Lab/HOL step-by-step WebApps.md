![Microsoft Cloud Workshop](images/ms-cloud-workshop.png)

Hands-on lab
Feb 2021

<br />

**Contents**

<br />

# **要約および学習目標**

### **事前準備**

- ローカル環境
  - Visual Studio または Visual Studio Code のインストール

    Visual Studio 2019  
    <https://visualstudio.microsoft.com/ja/downloads/>

    Visual Studio Code  
    <https://azure.microsoft.com/ja-jp/products/visual-studio-code/>

  - Git のインストール  
    <https://git-scm.com/>

  - Azure CLI のインストール  
    <https://docs.microsoft.com/ja-jp/cli/azure/install-azure-cli>

- GitHub

  - アカウントの作成  
    <https://github.com/>

- Microsoft Azure

  - ポータルへのアクセス  
    <https://portal.azure.com/>

<br />

# **GitHub リポジトリのフォーク**

  - Web ブラウザを起動し、ワークショップのリポジトリを表示  
    <https://github.com/hiroyay-ms/Git-Training-for-Beginner>

  - 画面右上の **fork** をクリック

    <img src="images/github-fork-01.png" />

  - リポジトリが複製されていることを確認

    <img src="images/github-fork-02.png" />

    ※ hiroyay-demo-org の箇所に自身の github アカウント名が表示されていることを確認

<br />

# **Azure Web Apps の作成～アプリケーションの展開**

## リソース グループの作成

  - Web ブラウザを起動し **[Azure ポータル](https://portal.azure.com)** を表示

  - 画面上部の "**＋リソースの作成**" をクリック

    <img src="images/create-resource.png" />

  - 検索ボックスに **Resource Group** と入力  
    表示される候補より **Resource Group** を選択

    <img src="images/resource-group-01.png" />

  - "**作成**" をクリック

    <img src="images/resource-group-02.png" />

  - **リソース グループ名** を入力し, **リージョン** を選択  
    "**確認および作成**" をクリック

    <img src="images/resource-group-03.png" />  
    ※リソース グループ名、リージョンは任意

  - 入力内容に不備がないことを確認し "**作成**" をクリック

    <img src="images/resource-group-04.png" />

  - リソース グループの作成を確認

    <img src="images/resource-group-05.png" />

## Web Apps の作成

  - **[Azure ポータル](https://portal.azure.com)** のホーム画面を表示

  - 画面上部の "**＋リソースの作成**" をクリック

    <img src="images/create-resource.png" />

  - **Web アプリ** を選択

    <img src="images/web-apps-01.png" />

  - **Web アプリの作成**  
    **基本** タブ
    - **リソース グループ**: 先の手順で作成したものを選択
    - **名前**: （任意）※インターネットに公開できるユニークな名前
    - **公開**: コード
    - **ランタイム スタック**: .NET Core 3.1 (LTS)
    - **オペレーティング システム**: Windows
    - **地域**: （任意）
    - **App Service プラン**: （新規作成）名前は任意
    - **SKU とサイズ**: Premium V3 P1V3

      <img src="images/web-apps-02.png" />  

      ※App Service プランは新規作成をクリックし、名前を入力  
      <img src="images/web-apps-03.png" />

      ※SKU とサイズは **サイズを変更します** をクリックし P1V3 を選択  
      <img src="images/web-apps-04.png" />

      必要事項を入力、選択後 "**次: 監視** をクリック

    **監視** タブ
    - **Applicatoin Insights を有効にする**: いいえ

      <img src="images/web-apps-05.png" />

      ※"**確認および作成**" をクリック

    **確認および作成** タブ

    - 入力内容に誤りがないことを確認し "**作成**" をクリック

      <img src="images/web-apps-06.png" />

  - リソースの展開が正常に完了したことを確認し、"**リソースへ移動**" をクリック

    <img src="images/web-apps-07.png" />

## Web Apps の展開設定

  - Web Apps の管理ブレードを表示  
    左側のメニューから "**デプロイ センター**" をクリック

    <img src="images/web-apps-08.png" />

  - "**設定**" をクリック

    <img src="images/web-apps-09.png" />

  - ソースから"**GitHub**" を選択し、"**承認する**" をクリック

    <img src="images/web-apps-10.png" />

  - GitHub アカウント名とパスワードを入力し、"**Sign in**" をクリック

    <img src="images/web-apps-11.png" />

  - GitHub リポジトリ、ブランチを選択
    - **組織**: GitHub アカウント名
    - **リポジトリ**: fork したリポジトリ名 (Git-Training-for-Beginner)
    - **ブランチ**: main

    <img src="images/web-apps-12.png" />

  - "**ファイルのプレビュー**" をクリック  
    ※GitHub から Azure Web Apps へアプリケーションを展開するワークフローの内容を確認

    <img src="images/web-apps-13.png" />

    内容を確認後 "**Close**" をクリックし、プレビュー画面を閉じる

  - "**保存**" をクリックし変更内容を反映  
    ※GitHub のシークレットに発行プロファイルを登録  
    ※GitHub Actions のワークフローを作成

    <img src="images/web-apps-14.png" />

## GitHub Actions ワークフローの構成

  - リポジトリを表示  
    "**Settings**" をクリック

    <img src="images/github-actions-01.png" />

  - "**Secrets**" をクリック  
    ※Repository secrets に発行プロファイル情報が登録されていることを確認

    <img src="images/github-actions-02.png" />

  - "**Code**" をクリック  
    **.github/workflows** へ移動し main_app_XXXX.yml を選択  
    ※ファイル名は作成した Web Apps の名前により異なります。

    <img src="images/github-actions-03.png" />

  - 鉛筆マークのアイコンをクリック

    <img src="images/github-actions-04.png" />

  - Editor が起動し、ワークフロー ファイル (.yml) の内容が表示

    <img src="images/github-actions-05.png" />

  - 11 行目を改行し、以下のコードを挿入

    ```
    env:
      APP_PATH: './src/Web'
    ```
    ※ASP.NET Core MVC のプロジェクト ファイルへのパスを追加

  - dotnet build コマンドを以下に変更

     ```
     dotnet build ${{ env.APP_PATH }} --configuration Release
     ```
     ※追加した変数を build の後に追加

  - dotnet publish コマンドを以下に変更

    ```
    dotnet publish ${{ env.APP_PATH }} -c Release -o ${{env.DOTNET_ROOT}}/myapp
    ```
    ※追加した変数を publish の後に追加

    <br />

    ※変更後のワークフロー ファイル（全文）
    ```
    ```

  - "**Start commit**" をクリック  
    "**Commit changes**" をクリックし、変更を反映

    <img src="images/github-actions-06.png" />

  - "**Actions**" タブをクリック

    <img src="images/github-actions-07.png" />

  - 起動しているワークフローを選択  
    ※ワークフローが push イベントをトリガーに起動するため、.yml ファイル保存時にワークフローが起動

    <img src="images/github-actions-08.png" />

  - ワークフローの実行状況を確認

    <img src="images/github-actions-09.png" />

    <img src="images/github-actions-10.png" />

  - 正常に終了することを確認

    <img src="images/github-actions-11.png" />

  - [**Azure ポータル**](https://portal.azure.com) を表示し、Web Apps の管理ブレードから "**概要**" を選択  
    "**URL**" をクリックし、新しいタブでアプリケーションを表示

    <img src="images/web-apps-15.png" />

<br />

### **参考情報**
- **[Azure リソースの名前付けおよびタグ付けの戦略を作成する](https://docs.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging)**

- **[名前付け規則を定義する](https://docs.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming)**

- **[Azure リソースの種類に推奨される省略形](https://docs.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations)**  

<br />

# Web アプリの更新～展開, KeyVault 参照の使用

## リポジトリのクローン

### Visual Studio Code によるリポジトリの複製

※[Visual Studio をご利用の場合はこちら](#visual-studio-によるリポジトリの複製)

  - Web ブラウザを起動し、GitHub リポジトリを表示  
    "**Code**" をクリックし URL をコピー

    <img src="images/git-clone-url-copy-01.png" />

  - Visual Studio Code を起動  
    画面左上のアイコンをクリックし Explorer を表示

    <img src="images/git-clone-vscode-01.png" />

  - "**Clone Repository**" をクリック

    <img src="images/git-clone-vscode-02.png" />

  - 画面上部に表示されるコマンド パレットにコピーした URL を貼り付け Enter キーを押下

    <img src="images/git-clone-vscode-03.png" />
  
  - エクスプローラーでリポジトリの複製先となるフォルダを選択（任意）  
    "**Select Repository Location**" をクリック

    <img src="images/git-clone-vscode-04.png" />

  - 複製完了後、画面下部にメッセージが表示  
    "**Open**" をクリック

    <img src="images/git-clone-vscode-05.png" />

  - "**src/Web**" に Web アプリケーションのソース コードが複製されていることを確認

    <img src="images/git-clone-vscode-06.png" />

### Visual Studio によるリポジトリの複製

  - Visual Studio を起動  
    "**リポジトリのクローン**" を選択

    <img src="images/git-clone-visual-studio-01.png" />

  - "**GitHub**" をクリック

    <img src="images/git-clone-visual-studio-02.png" />

  - "**ブラウザーでサインインします**" をクリック

    <img src="images/git-clone-visual-studio-03.png" />

    ※Web ブラウザーでサインインを実行  
    ※すでに GitHub にサインインしている場合はプロファイル ページが表示

  - クローンするリポジトリを選択し "**複製**" をクリック

    <img src="images/git-clone-visual-studio-04.png" />

  - ソリューション エクスプローラーにてコードが複製されたことを確認

    <img src="images/git-clone-visual-studio-05.png" />

## Web アプリの更新～ GitHub リポジトリへのプッシュ

### Visual Studio Code によるアプリケーションの更新

※[Visual Studio をご利用の場合はこちら](#visual-studio-によるアプリケーションの更新)

  - "**F5**" キーを押下し、アプリケーションを実行

  - "**appsettings.Development.json**" を追加

### Visual Studio によるアプリケーションの更新

## アプリケーション構成の追加

## KeyVault の作成

## シークレットの追加

## マネージド ID の作成

## KeyVault 参照の構成

<br />

### **参考情報**

- [**App Service と Azure Functions の KeyVault 参照を使用する**](https://docs.microsoft.com/ja-jp/azure/app-service/app-service-key-vault-references)