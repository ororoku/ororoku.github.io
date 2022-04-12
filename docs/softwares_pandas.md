# pandas 
- [Overview](#Overview)
- [Tips](#Tips)
  - [DataFrame](#dataframe)
  - [Data Transformation](#datatransformation)
  - [Group Operations](#groupoperations)
  - [Time Series](#timeseries)
  - [Connecting Databases](#connectingdatabases) 
- [Errors](#Errors)

## Overview

## Tips
### DataFrame
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

* 結合の仕方

  - merge データフレームに含まれる行を一つ以上のキーでマージ(SQLの結合操作と同等)
  - concat 軸に沿った連結、あるいは積み重ね
  - join 
  - append 

```Python
#
# dataディレクトリ内の全てのファイルを読み込んで結合させる
#

import glob
df = pd.DataFrame()

files = glob.glob("./data/*")

for file in files:
  tmp = pd.read_csv(file)
  df = pd.concat([df, tmp])
  del tmp
```


### DataTransformation
* 欠損データの確認
欠損がある行・列を抽出するやり方はそれぞれ以下の様になる。
```Python
df[df.isnull().any(axis=1)]
df.loc[:, df.isnull().any()]
```

* 文字列型のNoneTypeを数値型のNaNに変換する
```Python
df["test"] = df["test"].apply(lambda x: numpy.nan if x==None else x)
```

* 正規表現

例えば「AA1234567B」を「AA1234567(B)」にしたい場合は以下の様にする
```Python
tmp = df["x"].str.extractall(r'([A-Z]{2}.+)([A-Z].*)').reset_index()
tmp["x"] = tmp[0] + "(" + tmp[1] + ")"
tmp.drop(columns={"level_0", "match", 0, 1}, inplace=True)
df.rename(columns={"x":"x_org"}, inplace=True)
df = df.join(tmp)
```

* 条件抽出

query メソッドを使うと便利。以下の二つの書き方が同じになる
```Python
df.query("A == 0")
df.query("1 < A < 3")
df.query("1 < A and A < 3")

df[df["A"] == 0]
df[(1 < df["A"]) & (df["A"] < 3)] 
```

### GroupOperations
* groupbyによる集約
```Python
nunique # 一意の値をカウント
sum 
mean 
count
df.groupby("x").quantile(.75) # 上位25%パーセンタイル  
```

### TimeSeries
* 文字列と日付の変換
```Python
df['date'] = pd.to_datetime(df["yyyymm"], format='%Y%m') 
df['DateStr'] = df['DateObj'].dt.strftime('%d%m%Y')
df['yyyymm'] = df['date'].apply(lambda x: x.strftime('%Y%m'))
```

* ラグ変数の作り方

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

### ConnectingDatabases
* AWSとの連携 
  * sqlの実行結果をローカルで走らせたpythonのdataframeに取り込み
  * ローカルで走らせたpythonのdataframeをredshift上にtableとして生成
  * 参照 <https://dev.classmethod.jp/articles/amazon-redshift2pandas_with_psycopg2/>
* GCPとの連携
### 

## Errors
* SettingWithCopyWarningの対処
  * 概要 : DataFrameのスライスのコピーに対して値を代入しようとする際に発生
  * 対処 : copy()でコピーを生成
  * 参考 https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
* 空DFへの代入
  * 概要 : 空のDataFrameにintやfloatの値を代入してもdtypeがobjectになってしまう
  * 対処 : 空DFの生成直後にfillna(0)してNaNを無くしておく
  * 参考 : [Pandasで空DFを作って後からintを代入する件](https://pepper.is.sci.toho-u.ac.jp/pepper/index.php?%A5%CE%A1%BC%A5%C8%2FPandas%A4%C7%B6%F5DF%A4%F2%BA%EE%A4%C3%A4%C6%B8%E5%A4%AB%A4%E9int%A4%F2%C2%E5%C6%FE%A4%B9%A4%EB%B7%EF)
