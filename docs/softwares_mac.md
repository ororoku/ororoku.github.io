# MAC
- [Links](#Links)
- [Tips](#Tips)
- [Errors](#Errors)

## Links
よく使うリンク集

## Tips

### 導入ソフトウェアと設定
以下のソフトを導入している。
* Hammerspoon : ウィンドウを画面の好きな位置に集めることが出来る。設定ファイルと方法はhttps://gist.github.com/ororoku/ea8fec41bd787a5b0c57fe3b274fd2d0
* Clipy : クリップボードの拡張。コピーした履歴を一定数保存しShift + Command + Vで順番に貼り付け
　　　　　　　　　
### ショートカット
規定のショートカットでよく使うものは以下
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
