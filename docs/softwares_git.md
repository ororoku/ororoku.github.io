# Git
- [Links](#Links)
- [Tips](#Tips)
- [Errors](#Errors)

## Links
## Tips
### .gitignore
秘匿しておきたいファイルやキャッシュなどの一時ファイルなど git リポジトリのバージョン管理から特定のファイルやフォルダを除外したいときには .gitignore ファイルを作成する。リポジトリのルート直下に .gitignore ファイルを置くことによって、配下のディレクトリに再帰的に設定が適用される。

例えば macOSだと、finder のメタ情報を持つ .DS_store がディレクトリの至るところに作成されるので除外設定しておく。具体的には以下の様に記載する。
```
#カレントディレクトリとサブディレクトリから .DS_store を除外
.DS_store

#拡張子 .a の全てのファイルを除外
*.a

#上の設定の例外として lib.a は管理に含める。
!lib.a

#カレントディレクトリの TODO のみ除外。サブディレクトリ配下の TODO は除外されない
/TODO

#ディレクトリ build 配下の全てのファイルを除外
build/

#例えば、doc/notes.txt を除外するが, doc/server/arch.txt は除外しない
doc/*.txt

#doc/配下の全ての .pdf ファイルを除外する doc/a.pdf, doc/a/a.pdf なども含む
doc/**/*.pdf
```

自分で書いても良いが、出来合いのものを利用すると便利である。
* <https://www.gitignore.io/> は Python macOS などと入力することで生成してくれる。
* <https://github.com/github/gitignore> にも代表的なものがコレクションされている。

また、 gibo を使って以下の様に生成することも出来る。
```
gibo python >> .gitignore 
```

## Errors

### SAMLを使ったログイン
2018/03/26 

#### 症状
レポジトリを作り、ローカルPCにgit cloneしようとすると、以下のようなメッセージが出現して出来ない。
```
remote: this repository, you must use the HTTPS remote with a personal access token
remote: that has been whitelisted for this organization. Visit
remote: https://help.github.com/articles/authenticating-to-a-github-organization-with-saml-single-sign-on/ for more information.
```

#### 解決策
上記リンク先に行くと、いくつか選択肢があるので
https://help.github.com/articles/authorizing-a-personal-access-token-for-use-with-a-saml-single-sign-on-organization/
を選ぶ。メッセージにしたがい、Personal access tokenをAuthorize. 

これでclone出来るかと思いきや、メッセージが変わらない。これは、ローカルに保存されたkeychainの情報が邪魔してるからなので、
command + spaceでkeychain accessを呼び出し→ログインから全ての項目でgit を検索、削除
Personal Access tokensから該当のものを選んでedit→平文のパスワードにしてコピー→git cloneして貼り付け
これで上手くいった

