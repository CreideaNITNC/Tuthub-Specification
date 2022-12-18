# TutとTutHub間のProtocol

## 通信プロトコル

- HTTPS

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
