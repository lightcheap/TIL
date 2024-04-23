## 環境と状況
- Windows
- Laravel(PHP)
- Docker
- makefileで環境構築できるようになっている
- makeを使いたいけどできないよくわからない
- WSLでは使えるのになんで？

## 答え
のページ
[Window上のGitBashに追加する方法](https://gist.github.com/evanwill/0207876c3243bbb6863e65ec5dc3f058)

要するに使いたいなら入れないと使えないよ。
紹介されている内容ならgit bashで使えるようになる。
（元々WSLで環境構築するなら必要ないけど）

なので、
紹介されているサイトで
「make-〇.〇-without-guile-w32-bin.zip」を取得して、展開
紹介されているように展開したファイルを自PCのフォルダに移す。
同じフォルダがあるならそこにコピー。フォルダがないならフォルダごとコピー。
