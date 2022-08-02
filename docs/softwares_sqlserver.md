# SQL Server
本ページでは、Microsoft SQL Serverについて書く。
- [Overview](#Overview)
- [Tips](#Tips)
- [Errors](#Errors)
- [References](#References)

## Overview 
データベースを構築するには、以下の順番でSQLを実行する。
* DB作成
* テーブルの作成
* インデックスの作成
* データのinsert


### データベースの作成
### テーブルの作成


### インデックスの作成


### データのinsert

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
