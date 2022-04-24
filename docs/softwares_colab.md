# Title
本ページでは、Google Colabについて書く。
- [Overview](#Overview)
- [Tips](#Tips)
  - Kaggleとの連携
- [Errors](#Errors)


## Overview 
Colabは、Google Researchが提供するホスト型のJupyter Notebookサービスである。
コードは、各アカウント専用の仮想マシンで実行され、一定時間アイドル状態にある仮想マシンは削除される。


## Tips

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


[top](https://ororoku.github.io/) / [memo](https://ororoku.github.io/docs/memo.html)
