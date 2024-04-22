## 基本の入力
```
$get = fgets(STDIN);
```

## 前後空白や改行を取り除いて入力
```
$get = trim(fgets(STDIN));
```

## 複数の文字列の入力（区切りが空白や特定の文字列）
->返りは配列
```
$array = explode(" ", fgets(STDIN));
// $array = explode("/", fgets(STDIN));　など
```

## 複数の文字列の入力（区切りが空白や特定の文字列）
->返りは個別の変数
```
list($a, $b, $c) = explode(" ", fgets(STDIN));
```

## 文字列の文字を分割して代入
```
// 「あいう」という文字列が入力される場合
$array = str_split(fgets(STDIN));
Array
(
[0] => あ
[1] => い
[2] => う
)
// こういうやりかたもある
$array2 = str_split(fgets(STDIN), 2);
Array
(
[0] => あい
[1] => う
)
```

