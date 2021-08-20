# Python
- [Links](#Links)
- [Tips](#Tips)
  - [IPython](#ipython)  
  - [Jupyter Notebook](#jupyternotebook)
  - [Packages](#packages) 
- [Errors](#Errors)

## Links
よく使うリンク集

* 公式チュートリアル <https://docs.python.org/ja/3/tutorial/appetite.html>
* IPython Built-in magic commands <https://ipython.readthedocs.io/en/stable/interactive/magics.html>
* Python Package Index(PyPI) <https://pypi.org/>
* Julia, Matlabとの変換チートシート <https://cheatsheets.quantecon.org/>
* ゼロから学ぶPython <https://rinatz.github.io/python-book/>
* 東大のPython入門 <https://utokyo-ipp.github.io/> 
  * Colaboratoryによる演習 <https://colab.research.google.com/github/utokyo-ipp/utokyo-ipp.github.io/blob/master/colab/index.ipynb>

## Tips 

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
  * ``%whos``　現在宣言されている変数の一覧と型・内容を表示 
  * ``%time`` コードの実行時間測定。``%%time``でセルマジックとしても使える
  * ``%matplotlib inline`` pyplotなどで描写されたグラフをnotebook内に表示する。オプションをtkとした場合は別ウィンドウにインタラクティブなグラフを表示、notebookとした場合はインタラクティブなグラフをnotebook内に表示する。

これらの機能は、IPythonをバックエンドで使っているJupyter Notebookでも利用可能である。

### Jupyter Notebook
Jupyter Notebookとは、他の言語も移植可能にしたIPython Notebookの改良版である。
IPython Notebookとは、IPython専用のNotebookである。
Notebookとは、ブラウザ上でプログラムを動作させるための環境である。

まとめると、Jupyter Notebookとは、Python環境下で動作する、ブラウザ上でコードを実行したり他の言語ユーザーとシェアすることが出来る便利なツール、という理解で良いだろう。

よく冒頭に書いておくものは以下
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

* よく使うショートカット
  * notebook画面でEscキーを押してコマンドモードに入る -> hキーを押せばショートカット一覧がポップアップ
  * コマンドモードで``Shift + m`` 選択したセルの結合
  * コマンドモードで``d, d`` 選択したセルの削除
  * コマンドモードで``z`` セル削除の取り消し
  * エディットモードで``Shift + Tab``  Docstringの表示
  * エディットモードで``Command + /``  選択行のコメントon/off


また、アドオンをインストールすれば様々な拡張機能を使うことが出来る。

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

* 便利そうな拡張機能
  * Table of Content : マークダウンのhタグから目次の自動生成
  * Rise : notebookをスライド形式で表示させる

### Packages
#### pip
`pip`はインターネットで公開されているPythonパッケージを取得するためのパッケージ管理ツールである。
`pip`でPythonのパッケージ（ライブラリ）を管理している場合、`pip install -r requirements.txt`で指定のパッケージを一括でインストールすることが出来る。

よく使う設定ファイル`requirements.txt`の例は以下の通り。
```Python

```

現在の環境にインストールされたパッケージとバージョンを設定ファイルの形式で出力するには、`pip freeze`コマンドを使う。
ただ、これだと汚くなりやすいらしい。参照<https://www.kabuku.co.jp/developers/python-pipenv-graph>

#### Pipenv
`pipenv`は`pip`と仮想環境を作成するための`venv`の両方の機能を兼ね備えたサードパーティ製のパッケージ管理ツールである。
Pipenvを用いた仮想環境の構築
Pipenvがインストールされていること前提

プロジェクトのディレクトリ（新規に作成するか、既存のプロジェクトをcloneしてきたもの）に入って、以下を行う

1. Pipfileの作成

例えば、Pipfileを以下の様に書いて保存（既に存在する場合は省略）

```
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]
numpy = "*"
pandas = "*"
seaborn = "*"

[dev-packages]

[requires]
python_version = "3.6"
```
2. ライブラリのインストールと仮想環境内でのshellの起動

以下コマンドを実行
```
$ pipenv install 
$ pipenv shell
```
Pipfile.lockもここで作成もしくはupdateされる

* 参考

参考にしたページ<https://qiita.com/shinshin86/items/e11c1124e3e2e74556b8> requirement.txtで管理しているプロジェクトに導入する方法も書いてある。


## Errors
エラー備忘録

### import時
* featherライブラリはpip install featherでインストールできない <https://ykskks.hatenablog.com/entry/2019/06/27/132732>
