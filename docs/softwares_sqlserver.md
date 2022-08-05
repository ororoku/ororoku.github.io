# SQL Server
本ページでは、Microsoft SQL Serverについて書く。
- [Overview](#Overview)
- [Tips](#Tips)
- [Errors](#Errors)
- [References](#References)

## Overview 
以下、Windows PC上にデータベースを構築してデータを操作するための一通りの手順を解説する。

### データベースの作成
### テーブルの作成


### インデックスの作成


### データの操作（挿入・検索）


```
BULK INSERT test_table
FROM 'C:\Users\XXX\YYY\insert_data.csv'
WITH (FIRSTROW = 2,
    FIELDTERMINATOR = ',',
    ROWTERMINATOR='\n',
FIELDQUOTE = '"',
BATCHSIZE=250000,
FORMAT = 'CSV',
CODEPAGE = '65001',
    MAXERRORS=2);
```

正常にinsertされたかを確かめるため、終わったらカウント数の確認をしておこう。

## Tips

## Errors

## References
