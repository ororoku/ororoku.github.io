# IPython and Jupyter Notebook
- [Overview](#Overview)
  - [IPython](#ipython)
  - [Jupyter Notebook](#jupyternotebook)
- [Tips](#Tips)
  - よくNotebookの冒頭に書いておくもの
  - よく使うショートカット
  - 便利な拡張機能
- [Errors](#Errors)
- [References](#References)


## Overview 
### IPython
IPythonとは、Pythonの拡張された対話型シェルである。
以下の様な便利な機能がある。
* タブ補完
* オブジェクトイントロスペクション
  * 先頭か末尾に``?``をつけることでそのクラスのDocstringを確認できる
* システムコマンドの実行
  * 先頭に``!``をつけることでOSコマンド/シェルコマンドを実行できる
  * ``!ls`` などの標準出力を文字列のリストとしてPythonの変数に格納することができる
* マジックコマンドの利用
  * ラインマジック : 先頭に``%``をつけてコマンドを実行することで同一行のコマンドに適用される
  * セルマジック : 先頭に``%%``をつけてコマンドを実行することで同一セルのコマンドに適用される
  * ``%lsmagic`` 使用可能なマジックコマンドの一覧を表示
  * ``%quickref`` クイックレファレンス一覧を表示
  * ``%whos``　現在宣言されている変数の一覧と型・内容を表示。オプションとしてデータ型（DataFrameなど）を与えればそれに合致する変数のみを出力する。
  * ``%time`` コードの実行時間測定。``%%time``でセルマジックとしても使える
  * ``%matplotlib inline`` pyplotなどで描写されたグラフをnotebook内に表示する。オプションをtkとした場合は別ウィンドウにインタラクティブなグラフを表示、notebookとした場合はインタラクティブなグラフをnotebook内に表示する。

これらの機能は、IPythonをバックエンドで使っているJupyter Notebookでも利用可能である。

### Jupyter Notebook
Jupyter Notebookとは、他の言語も移植可能にしたIPython Notebookの改良版である。
IPython Notebookとは、IPython専用のNotebookである。
Notebookとは、ブラウザ上でプログラムを動作させるための環境である。

まとめると、Jupyter Notebookとは、Python環境下で動作する、ブラウザ上でコードを実行したり他の言語ユーザーとシェアすることが出来る便利なツール、という理解で良いだろう。
## Tips

### よくNotebookの冒頭に書いておくもの

```Python
# -*- coding: utf-8 -*-
import matplotlib.pyplot as plt
%matplotlib inline

import pandas as pd
import numpy as np

from IPython.core.display import display, HTML
display(HTML("<style>.container { width:100% !important; }</style>")) # セル幅を全画面に拡大
pd.set_option("display.max_columns",150) # Pandasのdataframeを150カラムまでは表示
```

### よく使うショートカット
* notebook画面でEscキーを押してコマンドモードに入る -> hキーを押せばショートカット一覧がポップアップ
* コマンドモードで``Shift + m`` 選択したセルの結合
* コマンドモードで``d, d`` 選択したセルの削除
* コマンドモードで``z`` セル削除の取り消し
* エディットモードで``Shift + Tab``  Docstringの表示
* エディットモードで``Command + /``  選択行のコメントon/off

### 便利な拡張機能
アドオンをインストールすれば様々な拡張機能を使うことが出来る。

よく使うものは以下である。
* Table of Content : マークダウンのhタグから目次の自動生成
* ??? : 変数の一覧を表示する
* Rise : notebookをスライド形式で表示する

インストール手順は以下。
```Shell
# a. アドオン群をインストールする
pip install jupyter_contrib_nbextensions

# b. aを設定画面で表示させるためのCSSファイル・jsファイルをインストールする
jupyter contrib nbextension install --user

# c. Jupyter Notebookのアドオン管理用のライブラリをインストールする
pip install jupyter_nbextensions_configurator

# d.cを有効化する
jupyter nbextensions_configurator enable --user
```
a~dの後、Jupyter Notebookを再起動すれば画面上部から「Nbextensions」が選択できるようになっている。



## Errors
## References

[top](https://ororoku.github.io/) / [memo](https://ororoku.github.io/docs/memo.html)
