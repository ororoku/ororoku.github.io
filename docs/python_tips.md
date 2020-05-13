# Python Tips
基本的に自分用

## 環境構築

### パッケージの一括インストール
pipでPythonのパッケージ（ライブラリ）を管理している場合、`pip install -r requirements.txt`で指定のパッケージを一括でインストールすることが出来る。

よく使う設定ファイル`requirements.txt`の例は以下の通り。
```Python

```

現在の環境にインストールされたパッケージとバージョンを設定ファイルの形式で出力するには、`pip freeze`コマンドを使う。

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
