# SQL Server
本ページでは、Microsoft SQL Serverについて書く。
- [Overview](#Overview)
- [Tips](#Tips)
- [Errors](#Errors)
- [References](#References)

## Overview 

以下、Windows PC上にデータベースを構築してデータを操作するための一通りの手順を解説する。

### インストール

SQL Server 2019 DeveloperエディションとSQL Server Management Studio (SSMS) をMicrosoftのページからダウンロードし、インストールする。

SSMSは、SQL Server から Azure SQL Database まで、SQL インフラストラクチャを管理するための統合環境であり、SQL Server とデータベースのインスタンスを構成、監視、および管理するためのツールが備わっている、とされている。

### ユーザーの作成

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

### Nullの取り扱いについて
「NULL値は集計またはその他のSET演算で削除されました。」という警告が出ることがある。

### 分析結果を新しいテーブルとして作成
Select結果からテーブルを作成するには、例えば以下の様に書く。
```
Select * into dbo.tmp From test_table
```

## Errors

### インストール時エラー「このディレクトリは圧縮されているか、圧縮されたディレクトリにあります。圧縮されていないディレクトリを指定してください。」

"C:\SQL2019"ディレクトリにSQL Server 2019 Developerエディションをインストールしようとして上記のエラーが起きた。OSはWindows10。

Cドライブのプロパティから「このドライブを圧縮してディスク領域を空ける」にチェックが入っていたのを外して解決。

### 出力したcsvにHeaderが付かない
Query -> Query Options -> Results から"include column headers ..."にチェックを入れて解決。

## References
