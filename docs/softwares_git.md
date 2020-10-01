# Git
- [Links](#Links)
- [Tips](#Tips)
- [Errors](#Errors)

## Links
## Tips
### gitignore
giboを使えば .gitignoreファイルを自動生成できる
```
gibo python >> .gitignore 
```

（自分用メモ）末尾に以下のものを手動で追加している
```
/.ipynb_checkpoints/
/__pycache__/
/data/
/fig/
/log/
/old/
/ref/
/tmp/
/src/credentials.py
```
### 

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

