# MAC
# Python
- [Links](#Links)
- [Tips](#Tips)
- [Errors](#Errors)

## Links
よく使うリンク集

## Tips
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
