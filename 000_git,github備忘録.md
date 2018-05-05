# gitとgithub関係の備忘録

**書き途中**

## 概要

gitとgithubを触り始めたので備忘録をまとめた。
コマンドを覚えるまでのチートシート。

## 動作環境

- Ubuntu 18.04 LTS
- xselコマンドを使用（ターミナルからのコピペなのでなくてもOK)

## 初回コミット前にやること

ユーザー名とメールアドレスを登録しないとコミットできない

```
username=hoge
useremail="${username}@gmail.com"
git config --global user.name "${username}"
git config --global user.email ${useremail}
```

## githubにssh鍵を登録

sshでgithubに接続する前準備。

```
# 鍵を保存するユーザーディレクトリへ移動
cd ~/.ssh

# 鍵を作成
ssh-keygen -t rsa

# 鍵の内容をクリップボードへコピー
cat id_rsa.pub | xsel -ib

## ブラウザで自分のgithubへアクセス
## 右上のユーザーアイコンからSettingsを押下
## SSH and GPG Keysを押下
## New SSH keyを押下
## Title(一覧で表示される名前)とKeyの内容を全て貼り付ける
## ブラウザの操作は終了

# sshで疎通できるか確認
## You've succsessfullyが表示されれば疎通OK
ssh -T git@github.com
```

## ssh形式でclone

ssh形式でcloneするとpush時にユーザー名、パスワードが聞かれなくなるので便利。

```
username=hoge
git clone git@github.com:${username}/repositoryname.git
```
