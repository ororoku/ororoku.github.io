# パソコン自作入門

本ページでは、パソコンを自作することを目標に、計算機を構成する各種ハードウェアとソフトウェアについて書く。

- [Hardwares](Hardwares)
  - Motherboard 
  - CPU
  - GPU
  - Momeory 
  - SSD and HDD
  - Network
  - Power
- [Softwares](Softwares)
  - OS
  - Security
- [Tips](#Tips)

## Hardwares

### GPU
グラフィックボードは、パソコンの映像を出力する役割を果たしている。
特に高性能なグラフィックボードになると、3Dゲームや高品質な映像鑑賞、CADなどの製図ソフトで製作を行う場合に必要となる。
グラフィックボードに搭載されている演算用のプロセッサ「Graphics Processing Unit」を略して「GPU」と呼ぶ。

## Softwares

## Tips 

### ランダウアーの原理
パソコンが熱くなる理由の一つは、情報と熱の関係からも考えることが出来るらしい。


### CPUの温度管理
CPUが適切に動作するための温度は65-90度である。
CPUには温度センサーが取り付けられており、Windows10では以下の方法で確認することが出来る。

* パフォーマンスモニターを用いた確認
  * コンピュータの管理 -> パフォーマンスモニター -> 上部の「+」アイコンをクリック
  * パフォーマンスモニターに表示する値を選択 : 「Thermal Zone Information」の中にある「Temperature」を選択して「追加」をクリック
  * 値はケルビンで取得される
* コマンドプロンプトを用いた確認
  * コマンドプロンプトを管理者として実行
  * `wmic /namespace:\\root\wmi PATH MSAcpi_ThermalZoneTemperature get CurrentTemperature` と入力
  * ケルビンを10倍した値が取得される
