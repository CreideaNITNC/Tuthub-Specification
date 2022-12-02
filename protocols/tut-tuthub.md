# TutとTutHub間のProtocol

## 通信プロトコル

- HTTPS

## フォーマット

- JSON

```ts
interface File {
    name: string
    type: 'image' | 'text'
    /** 画像の場合base64 encode*/
    content: string
}

interface Commit {
    id: UUID
    message: string
    files: File[]
}

interface Tag {
    id: UUID
    name: string
    commits: Commit[]
}

interface Data {
    tags: Tag[]
}
```

## tut push時

originに登録されているリンクに対して、POSTメソッドでJSONでDataを送信する。
