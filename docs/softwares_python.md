# Python
- [Links](#Links)
- [Tips](#Tips)
  - [Modules and Packages](#ModulesandPackages)
  - [Pipenv](#pipenv)
  - [jupyter](#jupyter)
  - [pandas](#pandas)
- [Errors](#Errors)

## Links
よく使うリンク集

* 公式チュートリアル <https://docs.python.org/ja/3/tutorial/appetite.html>
* Julia, Matlabとの変換チートシート <https://cheatsheets.quantecon.org/>
* ゼロから学ぶPython <https://rinatz.github.io/python-book/>

## Tips 

### Modules and Packages

#### pip
`pip`はインターネットで公開されているPythonパッケージを取得するためのパッケージ管理ツールである。
`pip`でPythonのパッケージ（ライブラリ）を管理している場合、`pip install -r requirements.txt`で指定のパッケージを一括でインストールすることが出来る。

よく使う設定ファイル`requirements.txt`の例は以下の通り。
```Python

```

現在の環境にインストールされたパッケージとバージョンを設定ファイルの形式で出力するには、`pip freeze`コマンドを使う。
ただ、これだと汚くなりやすいらしい。参照<https://www.kabuku.co.jp/developers/python-pipenv-graph>

#### Pipenv
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


### jupyter
Jupyter notebookの覚書き
* よく最初に書いておくもの
  * セル幅を全画面に拡大
  * Pandasのdataframeを150カラムまでは表示
```Python
# -*- coding: utf-8 -*-
import matplotlib.pyplot as plt
%matplotlib inline

import pandas as pd
import numpy as np

from IPython.core.display import display, HTML
display(HTML("<style>.container { width:100% !important; }</style>"))
pd.set_option("display.max_columns",150)
```
* 描画
  * 設定をリセット
  ```Python
  import matplotlib as mpl
  mpl.rcParams.update(mpl.rcParamsDefault)
  ```

### pandas
* AWSとの連携 
  * sqlの実行結果をローカルで走らせたpythonのdataframeに取り込み
  * ローカルで走らせたpythonのdataframeをredshift上にtableとして生成
  * 参照 <https://dev.classmethod.jp/articles/amazon-redshift2pandas_with_psycopg2/>
* GCPとの連携
* カラム名やインデックス名の変更
```Python
df.columns = ['a', 'b', 'c']
df.index = ['aa', 'bb', 'cc']
 
# 
# 東京、大阪、千葉の面積と人口
# 

df=DataFrame([[2190,13378],[1904,8850],[5157,6197]],
             columns=['area','population'],
             index=['Tokyooo','Osaka','Chibaaa'])
#---------------------------
#          area  population
# Tokyooo  2190       13378
# Osaka    1904        8850
# Chibaaa  5157        6197
#---------------------------
 
df.rename(columns = {'population':'pop'})
df.rename(index = {'Tokyooo':'Tokyo', 'Chibaaa':'Chiba'})
```
* 文字列と日付の変換・ラグ変数の作り方
```Python
df['date'] = pd.to_datetime(df["yyyymm"], format='%Y%m')
df['date_lag'] = df['date'] - pd.offsets.DateOffset(months=2)
df['yyyymm_lag'] = df['date_lag'].apply(lambda x: x.strftime('%Y%m'))
 
df['DateStr'] = df['DateObj'].dt.strftime('%d%m%Y')
```
* 文字列型のNoneTypeを数値型のNaNに変換する
```Python
df["test"] = df["test"].apply(lambda x: numpy.nan if x==None else x)
```

## Errors
エラー備忘録

### import時
* featherライブラリはpip install featherでインストールできない <https://ykskks.hatenablog.com/entry/2019/06/27/132732>
