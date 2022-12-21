# TutとTutHub間のProtocol

## 通信プロトコル

- HTTPS

## 認証

- Basic認証

### 手順

1. 『username:password』の文字列を作る
2. 1の文字列をbase64でencodeする
3. ヘッダに『Authorization: Basic 『2の文字列』を添付する

例

```ts
// ユーザ名: username
const username = "username";
// パスワード: password
const password = "password";

// [ユーザ名]:[パスワード]
const phrase = username+":"+password;

// base64エンコード
const base64encoded = window.btoa(phrase);

// ヘッダに追加
const headers = {
    "Authorization": "Basic " + base64encoded,
};

// リクエスト
await fetch("tuthub.top", {
    headers,
});
```

## フォーマット

- JSON

```ts
interface Picture {
    name: string
    bin: string // base64 encode
}

interface SourceCode {
    name: string
    content: string
}

interface Commit {
    id: UUID
    message: string
    pictures: Picture[]
    codes: SourceCode[]
}

interface Section {
    id: UUID
    name: string
    commits: Commit[]
}

interface Data {
    sections: Tag[]
}
```

## tut push時

originに登録されているリンクに対して、POSTメソッドでJSONでDataを送信する。
