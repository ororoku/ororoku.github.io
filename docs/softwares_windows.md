# Windows 

## Tips

### FTPサーバーに接続する
2022/10/02

Windows10でFTPサーバーに接続するには、File Explorerで「PC」を開き、右クリックして「ネットワークの場所を追加する」からFTPサーバー情報を追加する。
ただし、プロトコルの中でFTPは通信経路が暗号化されていないため、転送したデータ（パスワードなど）を盗まれる危険がある。サーバー側が対応していれば、SFTP、SCPといったプロトコルを利用した方が安全。

### Microsoft IMEを活用する
2022/09/28

Windows10の標準日本語入力システムであるMicrosoft IMEでは、予測入力機能を利用することが出来る。予測入力機能は、デフォルトでオンになっている。
たとえば、メモ帳などで「きょう」と入力すると、予測変換候補のリストに「2022年9月27日」と表示され、さらに「Tab」キーを押せば、和暦や曜日付きの日付など、いくつかのパターンで候補が表示される。ここで、予測変換の候補は、キー入力すると自動的に表示されるか「Tab」キーを押して表示させ、通常の変換時のようにキー入力後に「変換」キー（通常は「スペース」キー）を押すと表示されないので注意する必要がある。

参考 : [Windows10のMicrosoft IMEで日付や時刻を素早く入力する方法](https://4thsight.xyz/20835)

### MagicマウスをWindowsで使う
2022/09/18

公式では対応していないので、OSSを用いるやり方。

動作確認環境 :
* Apple Magic Mouse 2
* Windows 10

ステップ : 
1. Githubから[Brigadier](https://github.com/timsutton/brigadier)をダウンロード
2. コマンドプロンプトを起動し、`brigadier.exe -m MacBookPro16,3`を実行。7-Zipを入れる必要があると言われたのでそれもインストール。
3. フォルダ`BootCamp-061-51481`が作られるので入り、`$WinPEDriver$\AppleWirelessMouse\AppleWirelessMouse.inf`を右クリックしてインストール。

参考
* [Magicマウスは、Windows PCも使える](https://qiita.com/liu-wei/items/0355d6fbabd152c76ac2)
* [Windows 10 で Apple Magic Mouse 2 をフルに使う](https://heptech.fc2.page/2020/03/10/fully-utilize-apple-magic-mouse2-on-winndows10/)

### Magic KeyboardをWindowsで使う
2022/10/01 

検証環境
```
Apple Magoc Keyboard (Model A1644)
Windows10 Pro
```

Bluetooth接続でペアリング可能。
Windowsキーに相当するMacのキーは以下の通り。

| Windowsキー | Macキー |
| :--- | :--- |
| Windowsロゴ | command |
| Alt | option |
| Alt GR | option + control |
| Alt + 半角 | caps |
| アプリケーション | 該当なし |


## Links 
