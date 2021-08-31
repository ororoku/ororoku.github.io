# pandas 
- [Links](#Links)
- [Tips](#Tips)
  - [DataFrame](#dataframe)
  - [Data Transformation](#datatransformation)
  - [Group Operations](#groupoperations)
  - [Time Series](#timeseries)
  - [Connecting Databases](#connectingdatabases) 
- [Errors](#Errors)

## Links
* 10 minites to pandas <https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html#viewing-data>

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
### Data Transformation
* 文字列型のNoneTypeを数値型のNaNに変換する
```Python
df["test"] = df["test"].apply(lambda x: numpy.nan if x==None else x)
```

* 数値による条件抽出

query メソッドを使うと便利。以下の二つの書き方が同じになる
```Python
df.query("A == 0")
df.query("1 < A < 3")
df.query("1 < A and A < 3")

df[df["A"] == 0]
df[(1 < df["A"]) & (df["A"] < 3)] 
```

### Group Operations
* 結合の仕方
```Python
merge
concat
join
append
```

* groupbyによる集約
```Python
nunique # 一意の値をカウント
sum 
mean 
count
df.groupby("x").quantile(.75) # 上位25%パーセンタイル  
```

### Time Series
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

### Connecting Databases
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
