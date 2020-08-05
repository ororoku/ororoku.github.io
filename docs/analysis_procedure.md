# 分析の進め方
ここで説明するのは及第点の分析のやり方（もっと良いものはプロジェクトごとに考えてください）

研究における分析とビジネスにおける分析は、動機やResearch Questionが必ずしも必要ではない点が根本的に異なる。とはいえ共通する部分も多い。

## 背景と課題
* 背景
  * ビジネスモデルや、ストーリーを把握する
* 課題
  * ゴールは何なのか、いつまでに何がしたいのかを明らかにする
  * 自分の責任範囲と達成基準を明示的に合意する

## 分析設計
* モデル
  * 仮説
* 統計的な処理
  * 推定
  * 検定
* 予測
  * 予測精度の評価
* 考察
  * （ビジネス的な）含意

また、準備として以下のことを考える必要がある
* データ
  * RedshiftやBigQuery上にTableやViewを作成
* 分析環境
  * ローカルで分析する
  * ローカル（仮想環境）で分析する
  * サーバー上で分析する
* ディレクトリ構成
  * 自分がよくやる構成
  * Cookiecutterを使ってプロジェクトのテンプレートからプロジェクトを作ることも出来る

## よくやる分析
ソースコードはだいたいプライベート

* 判別分析
  * 目的変数の割合と説明変数の分布を重ねてプロット
  * ロジスティック回帰
  * Random Forest
  * XgBoost
* 自然言語処理
  * dataframeに対してlistを名寄せする <https://colab.research.google.com/drive/1Uv-TNiOKwPUSlqLZPxurgNUz2EIQT8MS#scrollTo=BluVjgsiX3GR>
* 因果推論
  * 交絡因子がある場合の因果効果推定 <https://colab.research.google.com/drive/1IMmdrQCK5aNvgJL65DyFMSrl9a-t7bN_>


## 参考資料
* CRISP-DM
* Kaggleなどで出来る人のコードを見る
  * Network : QuantEconのnotebook, <https://notes.quantecon.org/submission/5b32e9b0b9eab00015b89f7d>
  * EDAや構成 : Covid-19のが分かりやすかった



