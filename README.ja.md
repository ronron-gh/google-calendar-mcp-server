# Google Calendar MCP Server

[English README is here](README.md)

このドキュメントでは、Google Calendar APIを使用してカレンダーの内容を検索するMCPサーバーを構築するための手順を説明します。

## 前提条件

- [uv](https://github.com/astral-sh/uv)がインストールされていること
- Googleアカウントを持っていること

## 手順

### 1. Google Cloud プロジェクトを作成

Google Cloud コンソールまたは、下のリンクから、Google Calendar API を有効にします。

[APIの有効化](https://console.cloud.google.com/flows/enableapi?apiid=calendar-json.googleapis.com&hl=ja)

### 2. OAuth 2.0 同意画面を設定

Google Cloud コンソールのメニューまたは、下のリンクからブランディングに移動します。

[ブランディング](https://console.cloud.google.com/auth/branding?hl=ja)

1. アプリ名を設定します。
2. ユーザーサポートメールを設定します。
3. 利用できるユーザーの対象として「外部」を選択します。
4. デベロッパーの連絡先情報を設定します。

### 3. デスクトップ アプリケーションの認証情報を設定

Google Cloud コンソールのメニューまたは、下のリンクからクライアントに移動します。

[クライアント](https://console.cloud.google.com/auth/clients?hl=ja)

1. **クライアントを作成**をクリックします。
2. アプリケーション種類 -> デスクトップアプリ をクリックします。
3. 名前フィールドに、認証情報の名前を入力します。
4. 作成をクリックします。
5. ダウンロードした JSON ファイルを `credentials.json` として保存し、ファイルをプロジェクトのディレクトリに移動します。

### 4. テストユーザを作成

Google Cloud コンソールのメニューまたは、下のリンクから対象に移動します。

[対象](https://console.cloud.google.com/auth/audience?hl=ja)

1. **Add User**をクリックしてテストユーザ(自分のアカウント名)を追加します。

### 5. Python 環境のセットアップ

#### 仮想環境の作成

1. ターミナルまたはコマンドプロンプトを開きます。
2. プロジェクトディレクトリに移動します。
3. 仮想環境の設定と必要なライブラリをダウンロードします。

   ```sh
   uv sync
   ```

#### `token.json`の生成

1. 次のコマンドを実行して`token.json`ファイルを生成します：

   ```sh
   uv run generate_token.py
   ```

2. ブラウザが立ち上がり、Googleアカウントへのアクセス許可を求められます。許可を与えてください。
3. 認証が完了すると、プロジェクトディレクトリに`token.json`ファイルが作成されます。

#### MCPサーバを起動

1. 次のコマンドを実行してMCPサーバを起動します：

   ```sh
   uv run main.py
   ```

### トラブルシューティング

- **エラーが発生した場合**: エラーメッセージを確認し、必要に応じて依存関係を再インストールしたり、Google Cloud Consoleの設定を確認してください。
