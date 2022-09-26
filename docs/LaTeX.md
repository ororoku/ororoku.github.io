# LaTeX and BibTeX

## Overview 
LaTeXとは組版ソフトウェアである。
クラウド上でコンパイル可能なサービスであるOverleafも便利である。

## Tips 
### BibTeXのauthorフィールドの書き方

author={Yamashita, Taro and Oda, Hanako} のように，「姓, 名」または「名 姓」の順にかき，複数人を列挙するときは and で区切る。
ミドルネームがあるときは，「Last, First Middle」の形にする。多いときは最後に and others と書いておけば英語なら「et. al.」に，日本語なら「ほか」に変換される。
アクセント記号付きの文字を書きたい場合は author={G{\"o}del, Kurt} のように {} で囲う。

参考 : [【LaTeX】BibTeXにおけるbibファイルのかき方](https://mathlandscape.com/latex-bib/)

### Overleafでの日本語入力

コンパイラをpdfLatex -> Latexに変更

プロジェクト内にlatexmkrc

参考 : https://doratex.hatenablog.jp/entry/20180503/1525338512

—

## Links
* [BibTex Cleaner](https://bibtexcleaner.herokuapp.com/)
