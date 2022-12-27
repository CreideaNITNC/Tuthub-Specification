# TutHubサーバーのシーケンス設計

## TutHub Sign Up

チュートリアル制作者がTutHubにサインアップ

```mermaid
sequenceDiagram
actor creator as 作成者
participant form as Sign Up フォーム
participant SignController
participant SignService
participant SignRepository
participant DB
participant Session

creator->>form: name, mail, passwordを入力
form->>SignController: 送信
SignController->>SignService: サインアップ処理依頼
SignService->>SignRepository: 既存のmailまたはnameかを確認依頼
SignRepository->>DB: 確認クエリ
DB->>SignRepository: 結果
SignRepository->>SignService: 結果
alt mail, name重複アリ
    SignService->>SignController: エラー
    SignController->>creator: 失敗表示
else mail, name重複ナシ
    SignService->>SignRepository: 登録依頼
    SignRepository->>DB: INSERTクエリ
    DB->>SignRepository: 完了
    SignRepository->>SignService: 完了
    SignService->>SignController: 新規ユーザID
    SignController->>Session: Sessionログイン
    SignController->>creator: Homeへ画面遷移
end
```

## TutHub Sign In

チュートリアルアップロード者がTutHubにサインイン

```mermaid
sequenceDiagram
actor creator as 作成者
participant form as Sign In フォーム
participant SignController
participant SignService
participant SignRepository
participant DB
participant Session

creator->>form: name or mail, passwordを入力
form->>SignController: 送信
SignController->>SignService: サインイン処理依頼
SignService->>SignRepository: mail or nameに応じたユーザパスワードのハッシュ値引き出しを依頼
SignRepository->>DB: クエリ
DB->>SignRepository: 結果
SignRepository->>SignService: 結果
alt passwordとハッシュ値が不一致
    SignService->>SignController: エラー
    SignController->>creator: 失敗表示
else passwordとハッシュ値が一致
    SignService->>SignController: サインインユーザ
    SignController->>Session: Sessionログイン
    SignController->>creator: Homeへ画面遷移
end
```

## Tut Push

チュートリアル制作者がコマンドラインからリポジトリをpush

```mermaid
sequenceDiagram
actor CLI
participant auth as BasicAuthenticator
participant controller as TutController
participant service as TutPushService
participant cache as TutHubPageDataCache
participant repository as Repository
participant DB

CLI->>auth: Basic認証ヘッダとデータ
auth->>controller: 認証情報とデータ
controller->>service: 保存依頼
service->>repository: 保存依頼
repository->>DB: トランザクション開始
repository->>DB: リポジトリ内セクションDELETE
repository->>DB: セクションデータINSERT
repository->>DB: トランザクション終了
DB->>repository: 完了
repository->>service: 完了
service->>cache: キャッシュ破棄依頼
cache->>service: 完了
service->>controller: 完了
controller->>CLI: 201 Created
```

## TutHub-Page

チュートリアル閲覧者がデータをリクエスト

```mermaid
sequenceDiagram
actor browser as 閲覧者
participant controller as TutHubPageController
participant service as TutHubPageService
participant cache as TutHubPageDataCache
participant repository as Repository
participant DB

browser->>controller: 特定のセクションの内容を要求
controller->>service: 閲覧依頼
service->>cache: キャッシュ確認
cache->>service: キャッシュの有無
alt cacheにある
    cache->>service: データ
else cacheにない
    service->>repository: 問い合わせ
    repository->>DB: クエリ
    DB->>repository: 結果
    repository->>service: 結果
    service->>cache: キャッシュに保存
end
service->>controller: データ
controller->>browser: データ
```
