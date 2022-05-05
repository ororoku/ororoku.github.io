# Python
- [Overview](#overview)
  - [Coding Style](#codingstyle)
  - [Semantics](#semantics)
  - [Data Structures](#datastructures)
  - [Modules and Packages](#modulesandpackages) 
- [Tips](#Tips)
- [Errors](#Errors)


## Overview

### Coding Style
#### The Zen of Python

```
  Beautiful is better than ugly.
  Explicit is better than implicit.
  Simple is better than complex.
  Complex is better than complicated.
  Flat is better than nested.
  Sparse is better than dense.
  Readability counts.
  Special cases aren't special enough to break the rules.
  Although practicality beats purity.
  Errors should never pass silently.
  Unless explicitly silenced.
  In the face of ambiguity, refuse the temptation to guess.
  There should be one-- and preferably only one --obvious way to do it.
  Although that way may not be obvious at first unless you're Dutch.
  Now is better than never.
  Although never is often better than *right* now.
  If the implementation is hard to explain, it's a bad idea.
  If the implementation is easy to explain, it may be a good idea.
  Namespaces are one honking great idea -- let's do more of those!
```
Source : https://github.com/python/peps/blob/master/pep-0020.txt

#### 用語
* パスカルケース（アッパーキャメルケース） 
  * 最初の一文字と、各単語の最初の文字を大文字にする。 例: GetCurrentState
* キャメルケース（ローワーキャメルケース）
  * 各単語の最初の文字を大文字にする点はパスカルケースと同じだが、最初の一文字は小文字ではじめる。 例: getCurrentState
* スネークケース
  * 全部小文字で書き、単語と単語の間をアンダースコア _ でつなげる。 例: get_current_state
* ケバブケース
  * 全部小文字で書き、単語と単語の間をハイフン - でつなげる。 例: get-current-state

#### 命名規則
以下のものが推奨されている
| 名前をつけるもの | 命名規則 | 例 |
| ---- | ---- | ----  |
| 変数 | スネークケース | variable_name |
| 定数 | 全部大文字のスネークケース | CONSTANT_NAME |
| グローバル変数 | スネークケース | global_variable_name |
| 関数 | スネークケース | function_name |
| 関数の引数 | スネークケース | function_parameter_name |
| クラス | パスカルケース | ClassName |
| インスタンス変数 | スネークケース | instance_variable_name |
| メソッド | スネークケース | method_name |
| パッケージ | スネークケース | package_name |
| モジュール | スネークケース | module_name |

#### docstring
Sample 
```
def who(vardict=None):
    """
    Print the NumPy arrays in the given dictionary.
    If there is no dictionary passed in or `vardict` is None then returns
    NumPy arrays in the globals() dictionary (all NumPy arrays in the
    namespace).
    Parameters
    ----------
    vardict : dict, optional
        A dictionary possibly containing ndarrays.  Default is globals().
    Returns
    -------
    out : None
        Returns 'None'.
    Notes
    -----
    Prints out the name, shape, bytes and type of all of the ndarrays
    present in `vardict`.
    Examples
    --------
    >>> a = np.arange(10)
    >>> b = np.ones(20)
    >>> np.who()
    Name            Shape            Bytes            Type
    ===========================================================
    a               10               80               int64
    b               20               160              float64
    Upper bound on total bytes  =       240
    >>> d = {'x': np.arange(2.0), 'y': np.arange(3.0), 'txt': 'Some str',
    ... 'idx':5}
    >>> np.who(d)
    Name            Shape            Bytes            Type
    ===========================================================
    x               2                16               float64
    y               3                24               float64
    Upper bound on total bytes  =       40
    """
```
Source : https://github.com/numpy/numpy/blob/main/numpy/lib/utils.py

### Semantics
#### Operators
「=」演算子による代入はC++などの言語とは異なり参照渡しになる。
例えば
```Python
x = [1, 2]
y = x.copy()
y.append(3)

w = [1, 2]
z = w
z.append(3)

print(x, y)
print(w, z)
```

#### namespace
例えば、関数定義の外でxという変数を宣言していた場合、関数定義の中でxという変数を使おうとすると以下の様なルールが適用されるらしい。これは、バグの温床になりそう
* 関数定義の中でxを宣言しなかった場合 -> 外で宣言されたxを使う
* 関数定義の中でxを宣言した場合 -> 中で宣言されたxを使う

### Data Structures
Pythonのデータ構造には、以下の様なものがある。
* Sequencesと文字列


### Modules and Packages
モジュールとは、Pythonのファイル（.py）のことである。
例えば「sample.py」をimportすることで、「sample.py」に含まれる関数やクラスを利用することが出来るようになる。
パッケージとは、モジュールを複数集めたものである。同じフォルダの中に「__init__.py」が存在する。
ライブラリとは、パッケージを複数集めたものである。標準ライブラリと呼ばれるものはPythonをインストールすると一緒にインストールされ、print関数など事前に定義しなくても使えるものはこの中で定義されている。

#### pip
`pip`はインターネットで公開されているPythonパッケージを取得するためのパッケージ管理ツールである。
`pip`でPythonのパッケージ（ライブラリ）を管理している場合、`pip install -r requirements.txt`で指定のパッケージを一括でインストールすることが出来る。


現在の環境にインストールされたパッケージとバージョンを設定ファイルの形式で出力するには、`pip freeze`コマンドを使う。
ただ、これだと汚くなりやすいらしい。参照<https://www.kabuku.co.jp/developers/python-pipenv-graph>

#### Pipenv
`pipenv`は`pip`と仮想環境を作成するための`venv`の両方の機能を兼ね備えたサードパーティ製のパッケージ管理ツールである。
Pipenvを用いた仮想環境の構築
Pipenvがインストールされていること前提

プロジェクトのディレクトリ（新規に作成するか、既存のプロジェクトをcloneしてきたもの）に入って、以下を行う

1. Pipfileの作成

例えば、Pipfileを以下の様に書いて保存（既に存在する場合は省略）

```
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]
numpy = "*"
pandas = "*"
seaborn = "*"

[dev-packages]

[requires]
python_version = "3.6"
```
2. ライブラリのインストールと仮想環境内でのshellの起動

以下コマンドを実行
```
$ pipenv install 
$ pipenv shell
```
Pipfile.lockもここで作成もしくはupdateされる

* 参考

参考にしたページ<https://qiita.com/shinshin86/items/e11c1124e3e2e74556b8> requirement.txtで管理しているプロジェクトに導入する方法も書いてある。


## Tips
### 文字列の扱いで混乱しやすい点
```Python
print(type(("TEST")) == str,
type(["TEST"]) == str,
type({"TEST"}) == str, 
type("TEST") == str)

for i in ("TEST"):
  print(i)
for i in ["TEST"]:
  print(i)
for i in {"TEST"}:
  print(i)
for i in "TEST":
  print(i)
  
for i in ("TEST", "test"):
  print(i)
for i in ["TEST", "test"]:
  print(i)
for i in {"TEST", "test"}:
  print(i)
for i in "TEST", "test":
  print(i)
```

## Errors
エラー備忘録

### import時
* featherライブラリはpip install featherでインストールできない <https://ykskks.hatenablog.com/entry/2019/06/27/132732>
