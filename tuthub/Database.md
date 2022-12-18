# データベース

## ER図

```mermaid
erDiagram

users {
    UUID id PK
}

sign_users {
    UUID id PK
    string mail_address
    string password_hash
    UUID user_id FK
}

repositories {
    UUID id PK
    string name
    UUID user_id FK
    Date created_at
    Date updated_at
}

tags {
    UUID id PK
    string name
    int number
    UUID repository_id FK
    Date created_at
    Date updated_at
}

commits {
    UUID id PK
    int step
    string message
    UUID tag_id FK
    Date created_at
    Date updated_at
}

pictures {
    UUID id PK
    string filename
    data bin
    UUID commit_id FK
    Date created_at
    Date updated_at
}

source_codes {
    UUID id PK
    string filename
    string code
    UUID commit_id FK
    Date created_at
    Date updated_at
}

users ||--|| sign_users: ""
users ||--o{ repositories: ""
repositories ||--o{ tags: ""
tags ||--o{ commits: ""
commits ||--o{ pictures: ""
commits ||--|{ source_codes: ""
```

## 各テーブル

### users

### sign_users

- user_id: cascade delete

### repositories

- user_id: cascade delete
- user_id & name: 複合一意制約

### tags

- repository_id: cascade delete

### commits

- tag_id: cascade delete

### pictures

- commit_id: cascade delete

### source_codes

- commit_id: cascade delete
