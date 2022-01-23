## 勉強メモ



## #雑多

### クレデンシャル

IDやパスワードをはじめとするユーザなどの認証に用いられる情報の総称





## #centos

---

https://holidaynote.hatenablog.jp/entry/2018/04/21/224858

### java11を入れる

はまりポイント:yumでリポジトリの情報が取れるくせにインストールできない

→/etc/resolv.confにDNSの情報がなく、名前解決ができなかった。

(このconfファイル、再起動時に書き換わるらしい)

おそらくyumのリポジトリ自体はipでやりとりしているが中身のリンクはhostnameなため。

---

## #git 

### HEAD

現時点の最新のコミットを指す

### git config

```
#設定の一覧表示(指定なしの場合local,ただしgit管理されてない場合はglobal)
git config -l
```

### git add

```
#バージョン管理されていて変更があったリポジトリ内のすべてのファイルがadd(バージョイン管理されていないファイルは対象外)
git add -u
#変更があったリポジトリ内すべてのファイルがaddされる
git add -A
#変更があったカレントディレクトリ内のすべてのファイルがaddされる
git add .
```

### git log

```
#1行ずつ出せる
git log --oneline
#ある変更以降をみる。下記の例はorigin/masterからmasterまでの間
git log origin/master..master
```

### git diff

```
#作業ツリーとステージング
git diff
#ステージングとhead
git diff --staged
#作業ツリーとhead @はheadのエイリアス
git diff HEAD
git diff @
#コミット間 コミット指定はコミットidのユニークな頭文字でよい
git diff コミット1 コミット2
git diff コミット1 コミット2 -- ファイル
git diff コミット1 HEAD
#1個前
git diff @~1 @
git diff @^ @
#2個前
git diff @~2 @
git diff @^^ @
#ブランチ間
git ブランチa
git ブランチa ブランチb
git ブランチa:ファイル ブランチb:ファイル
#ブランチの1個前
git ブランチa^ ブランチa
```

### git ls-files

```
#ステージングのファイル一覧(sをつけるとハッシュも表示。ハッシュを使いshowで中を閲覧できる。)
git ls-files -s
```

### git show

```
#コミットの内容確認
git show
#コミット指定
git show @^
git show @^:ファイル名
#タグ指定
git show タグ名
```

### git reflog show master

```
#過去のあらゆるコミット履歴をみれる
git reflog show master
```



### git reset

```
#headの内容をステージにコピーする
git reset
#特定のファイルのみ
git reset -- ファイル
#作業ツリーの内容をheadに戻す(ステージングも戻る模様)
git reset --hard
#作業ツリーの内容を指定のコミットに戻す(ステージングも戻る模様)それ以降の変更は失う。(ハッシュ値が分かれば戻せる)
git reset --hard コミット
#headの位置をずらすだけで作業ツリーとステージングは無事。それ以降の変更はロストする。(ハッシュ値が分かれば戻せる)
git reset --soft コミット

```

### git checkout

```
#ステージングの内容を作業ツリーにコピーする
git checkout -- ファイル
#あるコミット時のデータをステージングと作業コピーにもってくる
git checkout コミット -- ファイル
#作業ディレクトリをある地点のcommitに戻す。HEADは戻さない
git checkout コミット .
#パスを指定しなかった場合HEADも移動してしまうので注意。reflogで戻してリカバリはできるが。。
git checkout コミット
#ブランチの切り替え　headが対象のブランチの先端と一体化する、中身がステージングと作業ツリーに取り出される
git checkout ブランチ
#ブランチの過去にHEADを移動する。
git checkout -b ブランチ名 コミット
#新しいブランチ
git checkout -b 新ブランチ
#新しいブランチに過去のコミットを吐く
git checkout -b 新ブランチ コミット
```

### git checkout -b ブランチ名 コミット

この方法で切り出すとheadが切り離された状態になる。(headが先端ではない)

その状態でコミットしてもどのブランチも伸ばさない。

そしてheadが離れると通常の方法ではアクセスできなくなる。

これを解消するには新しいブランチを切って、そこにチェックアウトする方法がある。

(ちなみに元のブランチに戻る分にはbranchにcheckoutすればよい)



### git mv

```
#ステージと作業ツリーの中で名前を変更する
git mv 元の名前　新しい名前
```

### git rm 

```
#作業ツリーとステージングからファイルを削除する
git rm ファイル
#ステージングのみファイルを削除する
git rm --chached ファイル
```

### git commit

```
#直前に行ったコミットをやり直す(push後にやると競合をおこしてしまうのでやっちゃだめ)
git commit --amend
```

### git revert

コミットを取り消す。ただし履歴は残り、取り消しした履歴も保持する。

```
git revert コミット
```

### .gitignore

バージョン管理にしないファイル群を書くと対象を無視してくれる。

```
#!を入れて書くと例外にしてくれる。下記はtest.logは無視しなくなる。
*.log
!test.log
```



### ブランチとは

* 一連のコミットの履歴
* その先端のコミットを指すポインタ



### git branch

```
#現在のブランチ一覧といまどこにいるかを示す
git branch
#コミットコメント情報がでる。
git branch -v
#ブランチ削除
git branch -d ブランチ
#ブランチ削除(強制)
git branch -D ブランチ
#リモート追跡ブランチの表示
git branch -r -v
#追跡を含むすべてのブランチの表示
git branch -a
#上流ブランチを設定する
git branch -u リモート追跡ブランチ
#上流ブランチの確認
git branch -vv
```



### git merge

```
#変更を受け入れるブランチに移動して実施する
git branch -v 
* ますたー
ブランチ
git merge ブランチ

#マージの取りやめ(コンフリクト時など)
git merge --abort

#3方向マージさせる
git merge --no-ff 相手ブランチ
```

### マージの種類

#3方向マージ

2つのブランチが分かれたコミット。

変更を取り込むブランチ、取り込まれるブランチでマージを行う

#早送りマージ

変更を取り込むブランチが取り込まれるブランチの祖先であるときだけ可能

(masterからprocが分岐して、procで開発が進む間masterが動かないとその状態になる)

マージコミットを作らずポインタだけ進めてしまうので原則コンフリクトが起きないで変更を取り込む

<u>デメリットとしては、マージの履歴が残らないのでどこでマージしたのかが分からなくなる。</u>



### git rebase

#todo



### git cherry-pick

つまみぐい

#todo



### タグ

人間のわかりやすい名前をコミットにつけることができる。

ブランチと違ってチェックアウトしてもheadは移動しない

#軽量タグ

コミットに名前を与えるだけ

```
#コミットをしていしなければHEADにつける
git tag タグ名
#コミット指定
git tag タグ名　コミット
#タグ一覧の表示
git tag
```

#注釈付きタグ

```
#aを付けると注釈をつけれらる
git tag -a タグ名
git tag -a タグ名　コミット
```



```
#タグの削除
git tag -d タグ
```



### リモートリポジトリ

githubとかで新規に切る。

```
#紐づけ　originは慣例らしい
git remote add origin URL
#確認
git remote -v
git remote get-url origin
```

### git clone

```
#リモートリポジトリから取得。こうした場合、originはurlにに紐づいている。
git clone URL
git clone URL ディレクトリ
```



### git fetch

リモートをローカルに反映させる。(headは動かない。追跡ブランチに反映される)

```
git branch origin master
```

ローカルに完全に反映させたい場合は以下を実施

```
git checkout ローカルブランチ
git merge --ff-only リモート追跡ブランチ
```

あるいはpullを使う。(こっちの方が一般的っぽい)

### git pull

現在のリポジトリをリモートブランチで更新する。

```
git chekuout Y
git pull origin X
```



pullで毎回リモートブランチ先を書くのはしんどいので以下の方法で上流ブランチを設定すると省略可能

クローンの時はクローン時のブランチが紐づけられてるっぽい

```
git branch -u リモート追跡ブランチ
#pushのついででもできる
git push -u リモート ローカルブランチ
```



### 集団開発の手法

```
#マスタにチェックアウト
git checkout master
#最新にする
git pull
#自分の作業ブランチ(fix)とmasterをマージする
giti merge --no-ff fix
#pushする
git push
→成功したら終了、失敗したらマージコミットを捨てる
git reset --hard @^
```





### 一般的な初動

```bash
# git管理スタート
git init 
git add *
git commit -m "first commit"
# ブランチ名作成
git branch -M main
# git紐づけ　これでoriginでアクセスできる。
git remote add origin https://github.com/tsukinana/studyMemo.git
# 管理物送信
git push -u origin main
→次回からgit pushだけでよい。(-uを付けると今のローカルとマスタを紐づけしたことになる)
```

### gitでバイナリ管理しないほうがいい理由

gitはテキストなどは圧縮して管理できるがバイナリはできない。

→svnと違って個人のpcにリポジトリをコピーする関係で肥大化がよろしくないため

### gitで毎回addがある理由

addはステージングにあげるコマンド。

ステージングにあげることでcommit予定のファイルを変更から守ることができる。

(addとcommitの間にレビューなどがない、個人開発ではあまり目立たない)

