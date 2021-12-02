# Unix / Linux
ここでは、LinuxやmacOSを含む、いわゆるUNIX風OSの使い方やコマンドについて説明する。

- [Overview](#Overview)
- [Tips](#Tips)
- [Errors](#Errors)
- [References](#References)

## Overview 
Unixは1969年にアメリカのベル研究所で開発されたOSである。その後BSD、SunOS、macOSなどに進化した。UNIXを模して開発されたLinuxがUNIX風OSのシェアの大部分を占める様になり、現在はmacOSを除いた他のUNIXは微々たるシェアを有するに過ぎない。
Windows 10では、WSL(Windows Subsystem for Linux)を有効化することで利用できる。

## Tips

### Commands 
* less 

`$ less *.txt`などで複数のファイルを同時に開く。:nで次のファイル、:pで前のファイルを表示。qで全ファイルを閉じる。

### Directory Structure
Linuxのディレクトリ構成は、[FHS(Filesystem Hierarchy Standard)](https://www.pathname.com/fhs/)という標準化仕様に基づいている。
Windowsと異なり、システム全体で一つのディレクトリツリーしか持たない。このため、追加する物理ディスクがある場合はルートディレクトリの配下ディレクトリとしてマウントすることになる。
重要なディレクトリとその役割を以下に挙げる。
* /bin 
* /dev 
* /etc 
* /home 
* /sbin 管理者ユーザー向けコマンド（shutdownなど）を置く
* /tmp 一時的なファイルを置く。
* /usr 各種アプリケーションとそれに付随するファイルを置く。内部にルートディレクトリと似た構造を持ち、配下にbinやsbin、etcなどをサブディレクトリとして持つ。
* /var 変化する(variable)データを置く。ログや電子メールなど

「新しいLinuxの教科書」参照


## Errors

## References
