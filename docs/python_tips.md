# Python Tips
基本的に自分用

## 環境構築

### パッケージの一括インストール
pipでPythonのパッケージ（ライブラリ）を管理している場合、`pip install -r requirements.txt`で指定のパッケージを一括でインストールすることが出来る。

よく使う設定ファイル`requirements.txt`の例は以下の通り。
```Python

```

現在の環境にインストールされたパッケージとバージョンを設定ファイルの形式で出力するには、`pip freeze`コマンドを使う。
ただ、これだと汚くなりやすいらしい。参照<https://www.kabuku.co.jp/developers/python-pipenv-graph>

### 仮想環境の構築（Pipenv）

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


## Jupyter notebook
よく最初に書いておくもの
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

## 判別分析

## 自然言語処理
* dataframeに対してlistを名寄せする <https://colab.research.google.com/drive/1Uv-TNiOKwPUSlqLZPxurgNUz2EIQT8MS#scrollTo=BluVjgsiX3GR>

## 因果推論
* 交絡因子がある場合の因果効果推定 <https://colab.research.google.com/drive/1IMmdrQCK5aNvgJL65DyFMSrl9a-t7bN_>

## その他
作った関数など
