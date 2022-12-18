# ディレクトリ
## 全体
作業ディレクトリ内に「.tut」というディレクトリを置き，その中にリポジトリに関する情報を全て置く。
## .tut
このディレクトリにはコミットを保存するdata.jsonとステージを保存するstage.jsonとpush先のURIなどの設定を保存するconfig.jsonがある。
### config.json
例
```json
{
    "remote": [
        {
            "name": "origin",
            "uri": "https://tuthub.top/cRVBJtcG"
        }
    ]
}
```
### data.json
[tut-tuthub.md](../protocols/tut-tuthub.md)に書かれているJSONそのもの
### stage.json
[tut-tuthub.md](../protocols/tut-tuthub.md)のFile[]にあたるJSON