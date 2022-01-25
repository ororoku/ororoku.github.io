# リンク集

- [Study](#Study)
- [Tools](#Tools)
- [Data](#Data)
- [Misc](#Misc)


## Study
体系的に身に付けるのに役立つオンラインのコンテンツ

* <https://library.oapen.org/> オープンアクセスの教科書が大量に置いてある。PDF形式でダウンロード可能

### CS, Math and Data Science
* [Structure and Interpretation of Computer Programs](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book.html)
  * 日本語版PDFも公開されている
* CS50 <https://cs50.harvard.edu/x/2021/>
  * 日本語版 <https://cs50.jp/>
* コーディング面接対策のために解きたいLeetCode 60問 <https://1kohei1.com/leetcode/>
* [ファインマン物理数学](http://www.thehugheslectures.info/wp-content/uploads/lectures/FeynmanHughesLectures_Vol5.pdf)
  * Lecture3 : ごちゃごちゃした関数の微分（対数微分の応用）
* <https://ja.wolframalpha.com/examples/mathematics/>
  * 数学の諸概念の解説とデモ
* 数理・データサイエンス教育強化拠点コンソーシアム http://www.mi.u-tokyo.ac.jp/consortium/e-learning.html
* [Deep Learning基礎講座演習コンテンツ 公開ページ | 東京大学松尾研究室 - Matsuo Lab](https://weblab.t.u-tokyo.ac.jp/deep-learning%E5%9F%BA%E7%A4%8E%E8%AC%9B%E5%BA%A7%E6%BC%94%E7%BF%92%E3%82%B3%E3%83%B3%E3%83%86%E3%83%B3%E3%83%84-%E5%85%AC%E9%96%8B%E3%83%9A%E3%83%BC%E3%82%B8/)

### Economics
* [QuantEcon](https://quantecon.org/)
  * Lecturesでは様々な経済学のモデルを実際に動かしながら学ぶことが出来る
  * Other Projectsも良い。QE Notesでは色々なケースのNotebookを見ることが出来る。右上のNotebooksから一覧を見れる
  * Julia, Matlabとの変換チートシートもある <https://cheatsheets.quantecon.org/>
* [Opportunity Insights](https://opportunityinsights.org/)
  * Raj.Chettyがやっているサイト
  * 論文のデータと解析コードなど
* "Social and Economic Networks: Models and Analysis" by Mat.Jackson <https://www.coursera.org/learn/social-economic-networks>

## Tools

### Linux
* ディレクトリ構造の標準化仕様　https://www.pathname.com/fhs/ 

### Python(official documents)
* Python公式チュートリアル <https://docs.python.org/ja/3/tutorial/appetite.html>
* Python Package Index(PyPI) <https://pypi.org/>
* Matplotlib tutorial https://matplotlib.org/stable/tutorials/index.html
* 10 minites to pandas <https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html#viewing-data>
* IPython Built-in magic commands <https://ipython.readthedocs.io/en/stable/interactive/magics.html>
* PEP8 : 推奨されるコーディング規約 <https://www.python.org/dev/peps/pep-0008/>
  * 日本語訳 <https://pep8-ja.readthedocs.io/ja/latest/> 
* Googleのコーディング規約 <https://google.github.io/styleguide/pyguide.html>
* Docstrings style guides
  * Google https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html
  * numpy https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard

### Python(Tips)
* グラフ作成のためのチートシートとPythonによる各種グラフの実装<https://qiita.com/4m1t0/items/76b0033edb545a78cef5>
* やさしいPython入門 <https://python.softmoco.com/basics/>
  * 命名規則を調べるのに使った 
* 東大のPython入門 <https://utokyo-ipp.github.io/> 
  * Colaboratoryによる演習 <https://colab.research.google.com/github/utokyo-ipp/utokyo-ipp.github.io/blob/master/colab/index.ipynb>
* ゼロから学ぶPython <https://rinatz.github.io/python-book/>

### Latex
* Overleaf : クラウド上で編集とコンパイルが出来るサイト 
* VS Codeでコンパイル出来る様に設定（MAC） 参考<https://qiita.com/Gandats/items/d7718f12d71e688f3573>

### Vim
* [Commands](https://www.radford.edu/~mhtay/CPSC120/VIM_Editor_Commands.htm)

### VS Code
* snippetなどの設定 参考<https://docs.microsoft.com/ja-jp/visualstudio/ide/walkthrough-creating-a-code-snippet?view=vs-2019>

### Regex
* <https://regex101.com/> 
  * テストしたい正規表現パターンと文字列を入力すると一致するか判定してくれる
  * PHP・javascript・Python・golangの４つの方言に対応
  * 内部処理をステップごとに見ることが出来るデバッグ機能もある
* [正規表現の"正規"とは何か気になったら正規表現の歴史を紐解くことになってしまった話](https://zenn.dev/yucatio/articles/0b554e59db0158)

## Data

### JP
* GDP統計・景気統計 <https://www.esri.cao.go.jp/index.html>
* 産業連関表 <https://www.soumu.go.jp/toukei_toukatsu/data/io/index.htm>
* Resas <https://resas.go.jp/> 
  * 経済産業省が提供する、産業構造や人口動態・人の流れなどの官民ビッグデータ。Tableauの様な可視化
* :newspaper_roll: IIPパテントDB <https://www.iip.or.jp/patentdb/>
  * 特許庁の整理標準化データを基に特許統計分析用に開発されたDB
* 産業生産性(JIP)など政策分析用データベース<https://www.rieti.go.jp/jp/database/index.html>

### US
* GDP統計など <https://www.bea.gov/>

### Cross-country
* Penn World Table <https://pwt.sas.upenn.edu/php_site/pwt_index.php>
* UN <http://unstats.un.org/unsd/nationalaccount/data.asp>
* AWS <https://registry.opendata.aws/>
* :newspaper_roll: PATSTAT <https://data.epo.org/expert-services/index.html>
  * European Patent Office (EPO)が提供する特許データ
* :newspaper_roll: Google Public Patent data <https://cloud.google.com/blog/products/gcp/google-patents-public-datasets-connecting-public-paid-and-private-patent-data>
* 🧑‍🎓 天体物理データシステム（Astrophysics Data System、ADS）<https://ui.adsabs.harvard.edu/>
  * NASAが提供する、天文学・物理学の論文DB
* 🧑‍🎓 JSTOR Data for research(DfR) <https://guides.smu.edu/jstordfr>

## Others
* 大学院生の掲示板 <https://www.econjobrumors.com/>
* 英語の表現を確認するのに便利なサイト <https://hypcol.marutank.net/ja/> ArXivの英語表現を検索して頻度別に表示
* [Langsmith Editor](https://editor.langsmith.co.jp/) アカデミック・ライティングのための執筆支援システム
* 手書き文字をLatexに変換できる <https://webdemo.myscript.com/views/math/index.html#>
* [青空文庫全文検索（非公式）](https://myokoym.net/aozorasearch/)
  * 単語や文章で検索でき、結果が整理されていて見やすい
  * 一応、Googleのsite検索を使っても同じことは出来る。検索窓で`我輩は site:www.aozora.gr.jp`など
