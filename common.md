## 勉強メモ



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

### originって何

リモートリポジトリURLの別名らしい

```
git remote get-url origin
```

で確認できる

### 初期動作

```bash
# git管理スタート
git init 
git add *
git commit -m "first commit"
# ブランチ名作成
git branch -M main
# git紐づけ
git remote add origin https://github.com/tsukinana/studyMemo.git
# 管理物送信
git push -u origin main
```

## gitでバイナリ管理しないほうがいい理由

gitはテキストなどは圧縮して管理できるがバイナリはできない。

→svnと違って個人のpcにリポジトリをコピーする関係で肥大化がよろしくないため

## gitで毎回addがある理由

addはステージングにあげるコマンド。

ステージングにあげることでcommit予定のファイルを変更から守ることができる。

(addとcommitの間にレビューなどがない、個人開発ではあまり目立たない)
