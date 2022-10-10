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

### ユーザーの作成とログイン
認証モードにはWindows認証とSQL Server認証がある。

SQL Server認証のユーザーを作成するのは、以下の手順でおこなう。
* 認証モードの変更 : SSMSを立ち上げてserverに接続-> Server Properties -> Securities -> Server authentificationを「SQL server認証モードとWindows認証モード」に変更
* Serverのrestart後、Security -> Logins -> New から認証を"SQL Server authentification"にして新しいユーザーを作成
* Serverを一度disconnectし、接続しなおす。認証をSQL Server認証に変えて、先ほど作ったユーザーでログインする


### データベースの作成
`CREATE DATABASE` ステートメントでデータベースの作成が可能である。
データベースファイル・ログファイルを配置するディスクの場所をオプションで指定して以下のように書く。

```
CREATE DATABASE test_db ON PRIMARY 
( NAME = 'test_db_dat', FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\test_dbdat.mdf' , SIZE = 20000MB , MAXSIZE = UNLIMITED , FILEGROWTH = 51200KB )
 LOG ON 
( NAME = 'test_db_log', FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\test_dblog.ldf' , SIZE = 1000MB , MAXSIZE = UNLIMITED , FILEGROWTH = 15360KB )
 COLLATE SQL_Latin1_General_CP1_CI_AS
GO
```

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

### 過去に実行したクエリの直近100件を表示する

```
SELECT TOP 100
	 qs.last_execution_time
	,st.text as query_text
	,qp.query_plan
FROM
	sys.dm_exec_query_stats as qs
CROSS APPLY
	sys.dm_exec_sql_text(qs.sql_handle) as st
CROSS APPLY
	sys.dm_exec_query_plan(qs.plan_handle) as qp
ORDER BY
	qs.last_execution_time desc
```

参考
* [SQL Serverで過去に実行したクエリを表示する](https://qiita.com/fuk101/items/00eb7963ed44988b5cf1)

### バッチからSQLファイルを実行
SSMSにプレインストールされているsqlcmdユーティリティを使って、コマンドプロンプトからSQLコマンドを実行できる。
例えばWindows認証で`insert.sql`を実行するバッチファイルは以下のように書く。
```
@echo off
sqlcmd -S localhost -d testDB -E -i insert.sql
pause
```

参照
* [【SQL Server】バッチファイルからsqlcmdコマンドを使用して、SQLを実行する](https://sqlserver.work/2020/06/27/%E3%83%90%E3%83%83%E3%83%81%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%8B%E3%82%89sqlcmd%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E3%80%81sql%E3%82%92%E5%AE%9F/)

### SQL Serverオンラインブックの開き方
クエリエディターのウィンドウ上で、例えば`CREATE DATABASE`というステートメントを選択してF1キーを押すと、SQL Serverオンラインブックの該当するトピックを開いて、全構文を見つけることが出来る。

### Nullの取り扱いについて
「NULL値は集計またはその他のSET演算で削除されました。」という警告が出ることがある。

### 分析結果を新しいテーブルとして作成
Select結果からテーブルを作成するには、例えば以下の様に書く。
```
Select * into dbo.tmp From test_table
```

## Errors

### リンク サーバー "(null)" の OLE DB プロバイダー "BULK" から必要なインターフェイス ("IID_IColumnsInfo") を取得できません。
未解決

### 一括読み込み: DataFileType が char に指定されていますが正しくありません。データ ファイルは Unicode 指定されているので、DataFileType は widechar と想定されます。
未解決

### 存在するテーブルなのに、SSMS上でInvalid object nameとなってしまう
CTRL+SHIFT+R で直った。

### インストール時エラー「このディレクトリは圧縮されているか、圧縮されたディレクトリにあります。圧縮されていないディレクトリを指定してください。」

"C:\SQL2019"ディレクトリにSQL Server 2019 Developerエディションをインストールしようとして上記のエラーが起きた。OSはWindows10。

Cドライブのプロパティから「このドライブを圧縮してディスク領域を空ける」にチェックが入っていたのを外して解決。

### 出力したcsvにHeaderが付かない
Query -> Query Options -> Results から"include column headers ..."にチェックを入れて解決。

## References
