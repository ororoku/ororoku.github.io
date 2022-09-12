# pandas 
- [Overview](#Overview)
  - [Series and DataFrame](#seriesanddataframe)
  - [Group Operations](#groupoperations)
  - [Time Series](#timeseries)
- [Tips](#Tips)
  - 色々なランダムサンプリング
  - groupbyで計算した結果をDataFrameの新しい列として代入する
  - ランダムな値を持つ列を追加する
  - ディレクトリ内のファイルを読み込んで結合させる
  - 一つでも欠損がある行や列を抽出する
  - 文字列型のNoneTypeを数値型のNaNに変換する
  - 正規表現を使ったデータ加工
  - queryメソッドを用いた条件抽出
  - 分散と標準偏差の計算について
  - データベースとの連携
- [Errors](#Errors)


## Overview
pandasはNumPyをベースに作成されたライブラリであり、SeriesとDataFrameというデータ構造を持つ。

### Series and DataFrame
Seriesは一次元の配列の様なオブジェクトであり、NumPyが持つデータ型のデータ配列とそれに関連付けられたデータラベルの配列（インデックス）を含む。
values属性とindex属性を使うと、データ配列とインデックスオブジェクトをそれぞれ取得することが可能である。
インデックスとデータ値がマッピングされた固定長の順序付きディクショナリと捉えることも出来、実際、ディクショナリをコンストラクタに渡してSeriesを作成することも出来る。

DataFrameはテーブル形式のデータ構造を持つ。

#### カラムとインデックス

以下の様にDataFrameを作成し、必要に応じてカラムとインデックスをrenameすることが出来る。
```Python
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

#### 結合

データの結合には以下の方法が用意されている。
  - merge データフレームに含まれる行を一つ以上のキーでマージ(SQLの結合操作と同等)
  - concat 軸に沿った連結、あるいは積み重ね
  - join 
  - append 

### GroupOperations
本節では、DataFrameのデータを集計するgroupbyメソッドについて説明する。
特定の列で集計するには`df.groupby('x')`の様にgroupbyメソッドの引数に列名を指定する。
この戻り値はDataFrameGroupByオブジェクトであり、集計結果を見るには以下の様な集計関数を使って取り出す必要がある。
```Python
df[['x','y']].groupby('x').mean() #xでグルーピングしたy列の平均値 
df[['x','y']].groupby('x').sum() #xでグルーピングしたy列の合計値 
df[['x','y']].groupby('x').count() #xでグルーピングした、NaNを含めないy列の合計数
df[['x','y']].groupby('x').size() #xでグルーピングした、NaNを含めたy列の合計数
df[['x','y']].groupby('x').nunique() #xでグルーピングした、y列のユニークカウント数
df[['x','y']].groupby('x').nth(0) #xでグルーピングした、y列の0番目のデータ
df[['x','y']].groupby('x').max() #xでグルーピングした、y列の最大値
df[['x','y']].groupby('x').min() #xでグルーピングした、y列の最小値
df[['x','y']].groupby('x').median() #xでグルーピングした、y列の中央値
df[['x','y']].groupby('x').quantile(0.75) #xでグルーピングした、y列の上位25%パーセンタイル
df[['x','y']].groupby('x').std() #xでグルーピングした、y列の標準偏差
df[['x','y']].groupby('x').var() #xでグルーピングした、y列の分散
```

ここに挙げたのは主なものだけである。メソッドの一覧は公式ドキュメントの[API reference](https://pandas.pydata.org/docs/reference/groupby.html)を参照。

### TimeSeries
pandasには時系列データを扱う機能も用意されていて、非時系列データと同じデータ構造で扱うことが出来る。

文字列と日付の変換
```Python
df['date'] = pd.to_datetime(df["yyyymm"], format='%Y%m') 
df['DateStr'] = df['DateObj'].dt.strftime('%d%m%Y')
df['yyyymm'] = df['date'].apply(lambda x: x.strftime('%Y%m'))
```

## Tips

### 色々なランダムサンプリング

`pandas.DataFrame.sample()`メソッドを使うと、データフレームから行や列を無作為抽出 (ランダムサンプリング)することが出来る。

```Python
df.sample()#無作為に1行を抽出
df.sample(3)#無作為に3行を抽出
df.sample(3, random_state=1)#無作為に3行を抽出, 乱数シードを固定
df.sample(frac=0.1)#無作為に10%を抽出
df.sample(10, replace=True, weights=[0.6, 0.1, 0.1, 0.1, 0.1])#(dfを5行のDataFrameとして)10回の重み付き復元抽出
```

### groupbyで計算した結果をDataFrameの新しい列として代入する
pd.DataFrameのgroupby関数で得られた集計値をDataFrameの新しい列として使いたい場合、`groupby().transform()`関数を用いるのが便利である。

```Python
import pandas as pd


df = pd.DataFrame(
    {
        "category": ["A", "A", "A", "B", "B"],
        "amount": [100, 300, 100, 200, 200],
    }
)
print(df)
"""
  category amount
0        A    100
1        A    300
2        A    100
3        B    200
4        B    200
"""

print(df.groupby("category").sum())
"""
category
A            500
B            400
"""

# 元のDataFrameと同じ行数で、対応する行の"category"列の値が含まれるグループの合計を返す
print(df.groupby("category").transform("sum"))
"""
   amount
0     400
1     400
2     500
3     500
4     500
"""

# 元のDataFrameに合計値を付与したい場合は次のようにできる
df["category_amount"] = df.groupby("category").transform("sum")["amount"]
print(df)
"""
  category  amount  category_amount
0        A     100              400
1        A     300              400
2        B     100              500
3        B     200              500
4        B     200              500
"""

# lambda関数と組み合わせて使うと、カテゴリの平均との差を出すといったことも出来る
print(df.groupby("category").transform(lambda x: x-x.mean()))
"""
       amount
0 -100.000000
1  100.000000
2  -66.666667
3   33.333333
4   33.333333
"""

```

別のやり方としては、`pd.merge()`で結合、辞書形式に変換して結合など。
```Python
# mergeで結合する場合
group_df = df.groupby("category").sum()
group_df.reset_index(inplace=True)
group_df.rename(columns={"amount": "category_amount"}, inplace=True)
print(pd.merge(df, group_df, on="category", how="left"))

# 辞書を作ってマッピングする場合
group_df = df.groupby("category").sum()
sum_dict = group_df.to_dict()["amount"]
print(sum_dict)
# {'A': 500, 'B': 400}
df["category_amount"] = df["category"].apply(sum_dict.get)
print(df)
```


参考にしたページ 

[pandas.DataFrameのgroupby関数で計算した結果を各行に展開する](https://analytics-note.xyz/programming/pandas-groupby-transform/)

### ランダムな値を持つ列を追加する

Seriesはnumpyの数列を引数にとって宣言することが出来るので、以下の様に書ける。

```Python
df['rand'] = pd.Series( np.random.random( len(df) ), index=df.index )
```

### ディレクトリ内のファイルを読み込んで結合させる

globモジュールを使うことで、引数に指定されたパターンにマッチするファイルパス名を取得することが出来る。
マッチングさせるパターンの書き方は、Unixシェルで使用される書き方と同様。

例えば以下の様にすると、カレントディレクトリにある全てのファイルを読み込んで結合させることが出来る。

```Python
import glob
df = pd.DataFrame()

files = glob.glob("./*")

for file in files:
  tmp = pd.read_csv(file)
  df = pd.concat([df, tmp])
  del tmp
```

### 一つでも欠損がある行や列を抽出する

anyメソッドを用いることで、一つでも欠損がある行・列を抽出することが可能である。
行と列について、それぞれ以下の様になる。

```Python
df[df.isnull().any(axis=1)]
df.loc[:, df.isnull().any()]
```

### 文字列型のNoneTypeを数値型のNaNに変換する

```Python
df["test"] = df["test"].apply(lambda x: numpy.nan if x==None else x)
```

### 正規表現を使ったデータ加工

例えば「AA1234567B」を「AA1234567(B)」にしたい場合は以下の様にする
```Python
tmp = df["x"].str.extractall(r'([A-Z]{2}.+)([A-Z].*)').reset_index()
tmp["x"] = tmp[0] + "(" + tmp[1] + ")"
tmp.drop(columns={"level_0", "match", 0, 1}, inplace=True)
df.rename(columns={"x":"x_org"}, inplace=True)
df = df.join(tmp)
```

### queryメソッドを用いた条件抽出

使用例

```Python
# 以下の書き方が同じ出力になる
df.query("A == 0")
df[df["A"] == 0]

df.query("1 < A < 3")
df.query("1 < A and A < 3")
df[(1 < df["A"]) & (df["A"] < 3)] 

# カラム名にスペースを含む場合
df.query('`B B` > A')  # B B列の値がA列の値より大きい行を抽出

# 条件を文字列で指定する場合
df.query('A == "test" ')  # A列の値が文字列"test"である行を抽出

# 欠損値の判定
df.query('A != A')  # A列の値が欠損である行を抽出
df.query('A == A')  # A列の値が欠損でない行を抽出

# リストを用いた抽出
df.query('A in (1, 2, 3)')  # A列の値が(1, 2, 3)のいずれかである行を抽出
x = [1,2,3]
df.query('A in @x')  # 変数を使用した場合
```

### 分散と標準偏差の計算について

分散と標準偏差について、numpyとpandasでは同じ名前の関数が与えられているが、デフォルト値が異なり、numpyではデータ数N、pandasではN-1で割っている。pandasのdescribe()のstdの値もN-1で割った不偏標準偏差である。以下のコードを実行してみよう。
```Python
import numpy as np
import pandas as pd

list_ = [ 1, 2, 3, 4, 5]
data_np = np.array(list_)
data_pd = pd.Series(list_)

print(np.var(data_np))
print(data_pd.var())
print(np.var(data_np, ddof=1))
print(data_pd.var(ddof=0))

print(np.std(data_np))
print(data_pd.std())
print(np.std(data_np, ddof=1))
print(data_pd.std(ddof=0))
```



### ラグ変数の作り方

例えば会社・月を複合主キーとするデータマートでnヶ月分のラグ変数と移動平均を作る場合
```Python
# 会社IDと年月で擬似的にCross join
ids = df["company_id"].unique()

tmp_ids = pd.DataFrame(
    {
        "company_id":ids,
        "crossjoinkey":1
    }
)

tmp_years = pd.DataFrame(
    {
        "Year" : [i for i in range(1994, 2013)], 
        "crossjoinkey" : 1
    }
)

df_cross = pd.merge(tmp_ids, tmp_years, how="outer")
del df_cross["crossjoinkey"]
  
# 愚直にずらして結合
# n = 1, single-variable
df['date_lag1'] = df['date'] - pd.offsets.DateOffset(months=1)
df['date_lag2'] = df['date'] - pd.offsets.DateOffset(months=2)
tmp = df[['company_id','date','x']].rename(columns={'date':'date_lag1','x':'x_lag1'})
tmp2 = df[['company_id','date','x']].rename(columns={'date':'date_lag1','x':'x_lag2'})
df = df.merge(tmp, on = ["company_id", "date_lag1"], how="left)
df = df.merge(tmp2, on = ["company_id", "date_lag2"], how="left)
df["x_ma1"] = (df["x_lag1"]+df["x_lag2"])/2

# shiftとrollingメソッドを使うやり方
# n = 5, multi-variables
tmp_all = pd.DataFrame()
for cat in set(df["company_id"]):
    tmp = df[df["company_id"] == cat]
    lag = pd.DataFrame() # ラグ変数
    ma = pd.DataFrame() # 移動平均
    for col in ('total_assets','cash_flow','other_var'): # ラグ変数と移動平均を作りたい変数のリスト
        for i in range(5):
            lag["{}_lag{}".format(col, i+1)] = tmp[col].shift(i+1)
            ma["{}_ma{}".format(col, i+1)] = tmp[col].shift(i+1).rolling(window=5).mean()
    tmp2 = tmp[["company_id", "date"]].join(lag)
    tmp2 = tmp2.join(ma)
    tmp_all = pd.concat([tmp_all, tmp2])
df = pd.merge(df, tmp_all, on = ["company_id", "date"], how = "left")
```

### データベースとの連携

AWSと連携するには以下の様にする。
  * sqlの実行結果をローカルで走らせたpythonのdataframeに取り込み
  * ローカルで走らせたpythonのdataframeをredshift上にtableとして生成
  * 参照 <https://dev.classmethod.jp/articles/amazon-redshift2pandas_with_psycopg2/>

## Errors
### SettingWithCopyWarningの対処
* 概要 : DataFrameのスライスのコピーに対して値を代入しようとする際に発生
* 対処 : copy()でコピーを生成
* 参考 https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy

### 空DFへの代入
* 概要 : 空のDataFrameにintやfloatの値を代入してもdtypeがobjectになってしまう
* 対処 : 空DFの生成直後にfillna(0)してNaNを無くしておく
* 参考 : [Pandasで空DFを作って後からintを代入する件](https://pepper.is.sci.toho-u.ac.jp/pepper/index.php?%A5%CE%A1%BC%A5%C8%2FPandas%A4%C7%B6%F5DF%A4%F2%BA%EE%A4%C3%A4%C6%B8%E5%A4%AB%A4%E9int%A4%F2%C2%E5%C6%FE%A4%B9%A4%EB%B7%EF)

### parse_datesでDateTime型として読み込まれないことがある
* 概要 : Google Colabにて、read_csvのオプションとしてparse_datesで指定した列がDateTime型として読み込まれないことがある
* 対処 : 未解決。年を使いたかったので文字列として読み込み、strアクセサを用いて最初の四文字を取得する（.str[:4]） 
