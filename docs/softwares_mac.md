# MAC
# Python
- [Links](#Links)
- [Tips](#Tips)
- [Errors](#Errors)

## Links
よく使うリンク集

## Tips

### ショートカット
* クイックルック（ファイルの中身を見る） : ファイルを選択してスペースキー（WindowsではAlt+P）
* Spotlight(全ファイルから検索) : Command + スペースキー
* 選択した単語をMac内蔵辞書から検索してその場でポップアップする : Command + Control + d

### Clipboard
Mac におけるクリップボード (コピペ領域)はペーストボードという名称で利用されている。標準で用意されたコマンドpbcopy, pbpasteを
パイプ、リダイレクトと組み合わせて以下の様に使うことが出来る。
```
$ echo test | pbcopy
$ pbpaste
test
$ echo test2 | pbcopy
$ pbpaste > ./testfile
$ cat ./testfile
test2
```

## Errors
