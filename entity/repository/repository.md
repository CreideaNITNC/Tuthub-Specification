# ドメインモデル TutHubRepository

## id

全てのリポジトリにサービス内で一意に割り振られるUUID

## name

ユーザごとに一意に割り振られるリポジトリ名。ユーザAがHelloリポジトリを持ち、ユーザBもHelloという名のリポジトリを持つことは可能だが、ユーザAが2つのHelloリポジトリを持つことはできない。

1文字以上の半角英数字またはハイフンで構成される

Webページのリンクに入る

## title

リポジトリが持つタイトル。Webページに表示される。TutHub.topで設定できる

デフォルトでnameが入る。文字はなんでも使用可能。ただし100文字以内（WebのCSSの都合上、上限を決めたいから）
