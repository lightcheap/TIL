## 状況
- ３つ職種別に分かれた求人テーブルがある。（DA,DB,DC）
- この３つのテーブルとcompanyテーブルを使用する
- それぞれが別テーブルで管理されている
- リレーションが貼っていない

## 実現したいこと
- companyテーブルのidにあてはまる３つの求人テーブルから求人を取得。
- company.idがどの職種の求人を作成しているか知りたい
- 求人数がどれだけか？は不要
- 職種ごとに検索できるようにしたい

## 参考ページ
https://techblog.recochoku.jp/5346
https://tigertaizo.hatenablog.com/entry/2021/12/01/200000

## これでいけるんじゃないかクエリ
FROM句の中で、companyと各職種をそれぞれJOINして検索する。
その際、各職種を表すカラムをクエリ内で暫定的に作成する。
それをUNIONする。
これをベースにしてSELECTとGROUPBYで集計する。

SELECT句のjob_typeには”da”,”db”,”dc”のどれかがそれぞれ入るようになる。
「GROUP_CONCAT(job_type) AS jobtype」で「da,db,dc」みたいに集計する土台を作る。
クエリの一番下のGROUPBYでd_id（事業所ID）毎に集計する。
カラムをGROUP_CONCATにしておかないと、上書きされ消えてしまうので注意。
```
SELECT
	GROUP_CONCAT(job_type) AS jobtype,
	d_id,
	dc_name,
	...(その他カラム)
FROM
(
	SELECT
	(CASE WHEN job.job_id IS NOT NULL THEN "da" ELSE NULL END) as job_type,
	company.d_id,
	company.dc_name,
	concat(lname, "", fname) as name,
	...(その他カラム)
	FROM company
	LEFT JOIN job AS job ON job.d_id = company.d_id
	WHERE company.del_flag = 0
	AND ...
	UNION
	SELECT
	(CASE WHEN jdt.job_id IS NOT NULL THEN "db" ELSE NULL END) as job_type,
	company.d_id,
	company.dc_name,
	concat(lname, "", fname) as name,
	...(その他カラム)
	FROM company
	LEFT JOIN job_dt_full AS jdt ON jdt.d_id = company.d_id
	WHERE company.del_flag = 0
	AND ...
	UNION
	SELECT
	(CASE WHEN dhp.job_id IS NOT NULL THEN "dc" ELSE NULL END) as job_type,
	company.d_id,
	company.dc_name,
	concat(lname, "", fname) as name,
	...(その他カラム)
	FROM company
	LEFT JOIN job_dh_part AS dhp ON dhp.d_id = company.d_id
	WHERE company.del_flag = 0
	AND ...
) AS jobunion
GROUP BY d_id LIMIt 0, 30
```
