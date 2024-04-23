## やりたいこと
Dockerで立ち上げたコンテナ内DBの中身をDBeaverで見れるようにしたい。
## やること
DBeaverを立ち上げ、
1. 新しい接続を作成
1. DBを選択
1. 接続設定（MySQL）
  - Server Host : 127.0.0.1
  - port        : docker-composeでの公開ポート docker desktopだと左側。.envに書くポートじゃない
  - Database   : Laravelだと.envに書くDB_DATABASE。DB名
  - ユーザー名   : Laravelだと.envに書いてる。ないならroot
  - パスワード   : Laravelだと.envに書いてる。ないなら空欄（だと思う）
