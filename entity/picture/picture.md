# ドメインモデル Picture

コミット時に添付できる画像データ

## id

サービス内で固有のID

## binary

画像のバイナリデータ

10MB(=10.000.000Byte)以内

## filename

.tutがあるディレクトリからの相対パス。ただし、拡張子は含めない

1文字以上100文字以内


## extension

列挙型。以下のcaseがある

- apng
- gif
- jpeg
- jpg
- jfif
- pjpeg
- pjp
- png
- svg
- webp
