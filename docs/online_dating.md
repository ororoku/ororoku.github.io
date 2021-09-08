# オンラインマッチングサービスまとめ
Covid-19によってオンラインマッチングサービスが盛り上がっているのでまとめてみた。
（騒動以前からあったものも含む）

## 既存のビジネス
* 業界のカオスマップ<https://lovetech-media.com/wp-content/uploads/2019/08/caosmap_pdf.pdf>
* 個人的に気になったもの
  * 職場が近くの3人でランチを食べられるサービス <https://c-table.co.jp/works/three/>
  * Zoom飲み : 結局流行っているのか？
  * Tinder : いつもの
  * CROSSME : 偶然の出会いに期待

## 経済学的特徴
マッチングやレコメンドといったものについての経済学的特徴は、二面市場であり、異なるステークホルダーが関係する問題であるという点である。
* 求職サービスの場合 : 求職者と企業
* 出会い系サービスの場合 : 男性と女性

プラットフォームの問題としては、両面のバランスを上手く取りながら収益をあげていく様な最適化問題となるだろう。

## 分権的か集権的か

### 分権的（お互いのリストを自由にブラウズしてコミュニケーションする）サービス
* Match.com
* Yahoo!Personals

### 集権的（"planner"がアルゴリズムによってマッチングさせる）サービス
最近はこちらが主流？
* eHarmony.com

## 論文紹介
出会い系サービスを経済学的に考察したものとして、
[Matching and sorting in online dating](https://pubs.aeaweb.org/doi/pdfplus/10.1257/aer.100.1.130)を紹介する。

### 概要
オンライン出会い系サイトのユーザー属性とインタラクションに関するデータを用いて、お互いの好みを推定し、Gale-Shapleyアルゴリズムを用いてマッチングを予測する。予測されたマッチは、出会い系サイトが達成した実際のマッチに似ており、実際のマッチはほぼ効率的である。

### 紹介スライド
2020/07/06 勉強会にて解説
<https://www.dropbox.com/s/tvihn0ohoh11w10/20200706_%E7%B5%8C%E6%B8%88%E5%AD%A6%E5%8B%89%E5%BC%B7%E4%BC%9A_%E5%A4%A7%E9%8C%B2.pptx?dl=0>

## 参考文献
一般的なサーチマッチング理論、労働問題、online dating serviceなどで以下の論文が参考になると思われる
* \citet{ADACHI2003182}は、サーチコストが小さい時、ベルマン方程式を解いて得られる均衡解が、Gale Shapley的な意味でStableになっていることを示した。AbstractのThe polarization of interests between men and women appears as in Gale--Shapley marriage problems; as agents of one sex become more selective about their mates, agents of the other sex lose.の辺りを、もう少し読んでみたい（が無料では読めない、、）
* [Matching and sorting in online dating](https://pubs.aeaweb.org/doi/pdfplus/10.1257/aer.100.1.130)
は、実際のデータからfrictionを推定している。ほぼefficientにマッチングしているということが分かった様だ。
* ベルマンオペレーターの不動点を求めるやり方は、Kamihigashi 2014や経済セミナーの最適化特集、尾山先生の動的計画法の資料<http://www.oyama.e.u-tokyo.ac.jp/econmath15/econmath15dp01RR.pdf>を参照
* Quant Econにも充実した説明がある

```
@article{ADACHI2003182,
	Abstract = {In a decentralized marriage market there are different types of men and women. Agents sequentially search for mating partners and meet bilaterally in a random fashion. Upon meeting, the paired agents complete mating if both agree, and separate and continue searching otherwise. The polarization of interests between men and women appears as in Gale--Shapley marriage problems; as agents of one sex become more selective about their mates, agents of the other sex lose. As search costs disappear, the set of equilibrium outcomes in a search model reduces to the set of stable matchings in a corresponding Gale--Shapley marriage problem.},
	Author = {Hiroyuki Adachi},
	Doi = {https://doi.org/10.1016/S0022-0531(03)00085-1},
	Issn = {0022-0531},
	Journal = {Journal of Economic Theory},
	Keywords = {Search, Two-sided matching, Stable matching, Gale--Shapley marriage problem},
	Number = {2},
	Pages = {182 - 198},
	Title = {A search model of two-sided matching under nontransferable utility},
	Url = {http://www.sciencedirect.com/science/article/pii/S0022053103000851},
	Volume = {113},
	Year = {2003},
	Bdsk-Url-1 = {http://www.sciencedirect.com/science/article/pii/S0022053103000851},
	Bdsk-Url-2 = {https://doi.org/10.1016/S0022-0531(03)00085-1}}


@article{hitsch2010matching,
  title={Matching and sorting in online dating},
  author={Hitsch, Gunter J and Horta{\c{c}}su, Ali and Ariely, Dan},
  journal={American Economic Review},
  volume={100},
  number={1},
  pages={130--63},
  year={2010}
}

@article{kamihigashi2014elementary,
  title={Elementary results on solutions to the Bellman equation of dynamic programming: existence, uniqueness, and convergence},
  author={Kamihigashi, Takashi},
  journal={Economic Theory},
  volume={56},
  number={2},
  pages={251--273},
  year={2014},
  publisher={Springer}
}
```
