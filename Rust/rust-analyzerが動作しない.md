## 状況
VSCodeに「rust-analyzer」を入れた。
以前は動いていたけど別の新規プロジェクトではうごいてくれない。
## 原因
settings.jsonに設定をかいてない。
以下を追加。
Cargo.tomlの場所を指定する。
```
{
    "rust-analyzer.linkedProjects": [
        "./Cargo.toml"
    ]
}
```
tauriとかだとこんなん。
```
    "rust-analyzer.linkedProjects": [
        "./src-tauri/Cargo.toml"
    ]
```
