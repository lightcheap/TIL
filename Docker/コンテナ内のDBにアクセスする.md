## 立ち上げたDBコンテナに入る
```
docker exec -i -t hogehoge-db bash
```

## コンテナに入ったらmysql ログイン
```
mysql -u root -p
# DB確認
show databases;
# テーブルを見るDBを選択
use fuga_db
# テーブル一覧を見る
show tables;
```
