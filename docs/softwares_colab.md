# Google Colab
本ページでは、Google Colabについて書く。
- [Overview](#Overview)
- [Tips](#Tips)
  - 一部のセルのみ編集して再実行
  - DataFrameの直接確認
  - Kaggleとの連携
- [Errors](#Errors)


## Overview 
Colabは、Google Researchが提供するホスト型のJupyter Notebookサービスである。
コードは、各アカウント専用の仮想マシンで実行され、一定時間アイドル状態にある仮想マシンは削除される。


## Tips

### きれいな目次の作り方
テキストセルに複数行書いても、目次では一つの見出しにまとめられる。

### 一部のセルのみ編集して再実行
一部のセル内容だけを一時的に変更して再実行したい時、以下の方法が便利である。
- 「表示」→「コードの実行履歴」を押すと右側にセルごとの実行履歴が表示される
- セルの左上に「スクラッチセルにコピー」が出ているので、それを押すと新しく「スクラッチセル」タブが開く
- 元のファイルに影響を与えずにスクラッチセル上で編集・再実行することが出来る

### DataFrameの直接確認

Colab内でdata_tableパッケージをimportすることで、以下の操作を実行しながらDataFrameを直接確認することが出来る。表示できるのは2万行までという制限がある。
- 指定列でのソート
- 正規表現を使ったフィルター
- 範囲を指定して検索
- ページ分けして全データを表示

コードの例は以下。
```Python
from google.colab import data_table
data_table.enable_dataframe_formatter()
 
from vega_datasets import data
cars = data.cars()
 
cars
```

### Kaggleとの連携

KaggleとGoogle ColabはどちらもGoogleのサービスでGCSを用いているため、連携が容易である。
Code Competitionは推論の実行をKaggleのNotebook環境で行わないといけない制約がある（後述のリンクを参照）が、Prediction CompetitionであればKaggleのデータをダウンロードし、submitするまでの一連の分析をcolab上で行うことが可能であると思われる。

__手順__
1. Kaggleのユーザーアカウントページからkaggle.jsonをダウンロードする
2. ColabのNotebookを実行し、kaggle.jsonをアップロードする
3. 分析を回し、予測結果をsubmitする

__Notebookの例__

Colab Notebookで以下を実行することで、TitanicのデータをColabにダウンロードしsample submitを行うことが出来る。
```Python
from google.colab import files
files.upload() # upload kaggle.json
!mkdir -p ~/.kaggle
!cp kaggle.json ~/.kaggle/
!pip install kaggle
!chmod 600 /root/.kaggle/kaggle.json

!kaggle datasets list
!kaggle competitions list
!kaggle competitions download -c titanic
!unzip /content/titanic.zip
!kaggle competitions submit -c titanic -f gender_submission.csv -m "submit from colab"
```

__エラー__
- `403 - Forbidden` 自分がjoinしていないcompetitionのデータをColabにダウンロードしようとした場合
- `400 - Bad request` code competition （コードコンペ）にColabからsubmitしようとした場合

__参考__
- [Colab で Kaggle (N番煎じ)](https://zenn.dev/mst8823/articles/da505dcf45474f)
  - code competition でサブミットするやり方
  - パイプラインの作り方も勉強になる
- [colabでkaggleのdatasetをマウントする](https://zenn.dev/karunru/articles/a8f394d7a859b7)
  - GCS経由のやり方
- https://github.com/Kaggle/kaggle-api

 

## Errors

### Tab補完がきかない

ツール -> 設定 -> 編集者 から 「コード入力時の候補を自動的に表示する」のチェックを外すと、機能するようになった。

### pandas_profiling.ProfileReportを使うとconcat() got an unexpected keyword argument 'join_axes'エラー

`!pip install -U pandas_profiling`でpandas_profilingのversionをupgradeすると解決

[top](https://ororoku.github.io/) / [memo](https://ororoku.github.io/docs/memo.html)
