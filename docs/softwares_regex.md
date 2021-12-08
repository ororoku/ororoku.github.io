# 正規表現
本ページでは、正規表現（Regular Expression）の説明と、よく使うものを置いておく。

- [Overview](#Overview)
- [Tips](#Tips)
- [Errors](#Errors)
- [References](#References)


## Overview 
[Wikipediaの説明](https://ja.wikipedia.org/wiki/%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE)によれば、正規表現とは、文字列の集合を一つの文字列で表現する方法の一つである。
もともと正規表現は形式言語理論において正規言語を表すための手段として導入された。形式言語理論では、形式言語が正規言語であることと正規表現によって表せることは同値である。
その後、テキストエディタなどのアプリケーションで、マッチさせる文字列を探索するために使われる様になった。その際、表せるパターンの種類を増やすために本来の正規表現にはないさまざまな記法が新たに付け加えられた。
このような拡張された正規表現には正規言語ではない文字列も表せるものも多く、ゆえに正規表現という名前は実態に即していない面もあるが、伝統的に正規表現と呼ばれ続けている。

歴史的には、
チューリング機械 -> 有限オートマトン -> ニューラルネットワーク -> 言語学者チョムスキーによる文法分類-> 数学者クリーネによる正規表現の定義 -> 再びチョムスキーによる正規文法の
定義、と進展してきた様だ。

ほとんどの形式で、正規表現を構築するのに以下の演算子を提供している。
* 選言(or)
* グループ分け(grouping)
* 量化(quantification)

## Tips
### ()と$でマッチした内容を記録して置換
例えば、以下の様に検索して置換することが出来る。
```
文字列 : display(pd.read_csv("Test.txt",sep="\t", nrows=5))
置換後文字列 : my_function("Test.txt")

Find : display\(pd\.read_csv\((.*),sep="\\t", nrows=5\)\)
Replace : my_function($1)
```

## Errors

[top](https://ororoku.github.io/) / [memo](https://ororoku.github.io/docs/memo.html)

## References
* <https://regex101.com/> 
  * テストしたい正規表現パターンと文字列を入力すると一致するか判定してくれる
  * PHP・javascript・Python・golangの４つの方言に対応
  * 内部処理をステップごとに見ることが出来るデバッグ機能もある
* [正規表現の"正規"とは何か気になったら正規表現の歴史を紐解くことになってしまった話](https://zenn.dev/yucatio/articles/0b554e59db0158)
