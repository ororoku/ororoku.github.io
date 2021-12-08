# Unix / Linux
ここでは、LinuxやmacOSを含む、いわゆるUNIX風OSの使い方やコマンドについて説明する。

- [Overview](#Overview)
- [Tips](#Tips)
- [Errors](#Errors)
- [References](#References)

## Overview 
Unixは1969年にアメリカのベル研究所で開発されたOSである。その後BSD、SunOS、macOSなどに進化した。UNIXを模して開発されたLinuxがUNIX風OSのシェアの大部分を占める様になり、現在はmacOSを除いた他のUNIXは微々たるシェアを有するに過ぎない。
Windows 10では、WSL(Windows Subsystem for Linux)を有効化することで利用できる。

### Directory Structure
Linuxのディレクトリ構成は、[FHS(Filesystem Hierarchy Standard)](https://www.pathname.com/fhs/)という標準化仕様に基づいている。
Windowsと異なり、システム全体で一つのディレクトリツリーしか持たない。このため、追加する物理ディスクがある場合はルートディレクトリの配下ディレクトリとしてマウントすることになる。
重要なディレクトリとその役割を以下に挙げる。
* /bin コマンドの実行ファイルが置かれる。
* /dev ハードウェア（キーボードやディスクなど）をファイルとして扱える様にした、デバイスファイルが置かれる。/dev/nullや/dev/randomは特別に用意された疑似デバイスファイルである。
* /etc アプリケーションの設定（コンフィグ）ファイルが置かれる。
* /home ユーザーごとに割り振られるホームディレクトリが配置される。
* /sbin 管理者ユーザー向けコマンド（shutdownなど）の実行ファイルが置かれる
* /tmp 一時的なファイルが置かれる。
* /usr 各種アプリケーションとそれに付随するファイルが置かれる。内部にルートディレクトリと似た構造を持ち、配下にbinやsbin、etcなどをサブディレクトリとして持つ。
* /var ログや電子メールなど、変化する(variable)データが置かれる。

## Tips

### 複数ファイルを同時にless
`$ less *.txt`などで複数のファイルを同時に開く。:nで次のファイル、:pで前のファイルを表示。qで全ファイルを閉じる。

## Errors

## References
* 「新しいLinuxの教科書」
