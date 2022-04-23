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

Kaggleのデータをダウンロードし、submitするまでをcolab上で行うことが可能である。

手順
1. Kaggleのユーザーアカウントページからkaggle.jsonをダウンロードする
2. ColabのNotebookを実行し、kaggle.jsonをアップロードする
3. 分析を回し、予測結果をsubmitする

Notebookの例
'''Python
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
'''


エラー
- `403 - Forbidden` 自分がjoinしていないcompetitionのデータをColabにダウンロードしようとした場合
- `400 - Bad request` code competition （コードコンペ）にColabからsubmitしようとした場合

参考
- https://zenn.dev/mst8823/articles/da505dcf45474f
  - code competition でサブミットするやり方
- https://dreamer-uma.com/kaggle-api-colab/
  - Kaggle Datasetにファイルをアップロードするやり方（学習をGoogle Colabで行い、推論のみKaggle notebookで行う場合など）
- https://qiita.com/katsu1110/items/a8d508a1b6f07bd3a243
- https://github.com/Kaggle/kaggle-api

 

## Errors


[top](https://ororoku.github.io/) / [memo](https://ororoku.github.io/docs/memo.html)
