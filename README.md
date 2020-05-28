# 🥭 git-staging-flow

## デプロイ先の前提

`メインとなるブランチたち` はそれぞれ一つずつデプロイする先（たとえばサーバー）があるとします

## 🍗 メインとなるブランチたち

### develop ブランチ

開発用

状況によっては複数個作られる場合がある

### staging ブランチ

QA や、お客さん確認など、開発者以外の方用

状況によっては複数個作られる場合がある

### production ブランチ

本番用

基本的に一つしかない

## 🍜 作っては削除されるブランチたち

### feature/* ブランチ

新機能の実装で `develop` ブランチから作成されます

### fix/* ブランチ

QA でバグがあった場合で `develop` ブランチから作成されます

### hotfix/* ブランチ

本番でバグがあった場合に `production` ブランチから作成されます

## 🥘 開発をするときのフロー

develop ブランチ -> feature ブランチ -> develop ブランチ

1. `develop` ブランチから `feature/first` ブランチを作成する
1. `feature/first` で作業をし **commit** する
1. 作業が完了したらローカルの `feature/first` ブランチを、リモートに **push** する
1. github.com のリポジトリページに行きプルリクエストを作成する
    * into `develop` from `feature/first`
1. プルリクエストのレビューを **Reviewers** から受ける
1. **Reviewers** が **approved** する
1. プルリクエストをマージする
1. ここで `develop` ブランチが **デプロイ** されるイメージ
1. `feature/first` ブランチを delete する

```
*   d87f0c9 (origin/develop) Merge pull request #1 from hisasann/feature/first
|\
| * 361dd3f (origin/feature/first, feature/first) first commit to feature/first
|/
* a34f262 (origin/staging, origin/production, staging, production) first commit
```

## 🥧 QA やお客さん確認のためのフロー

develop ブランチ -> staging ブランチ

1. github 上で **New pull request** をクリックする
1. base: `staging` ブランチ <- `develop` ブランチを選択する
1. タイトルやコメントを書く
1. **Create pull request** をクリックする
    * into `staging` from `develop`
1. **Merge pull request** をクリックする
1. **Confirm merge** をクリックする
1. ここで `staging` ブランチが **デプロイ** されるイメージ
1. [Branches](https://github.com/hisasann/git-staging-flow/settings/branches) で `develop`, `staging` ブランチを保護しているのでブランチの削除はできません

## 🍝 本番へのデプロイフロー

staging ブランチ -> production ブランチ

1. github 上で **New pull request** をクリックする
1. base: `production` ブランチ <- `staging` ブランチを選択する
1. タイトルやコメントを書く
1. **Create pull request** をクリックする
    * into `production` from `staging`
1. **Merge pull request** をクリックする
1. **Confirm merge** をクリックする
1. [Branches](https://github.com/hisasann/git-staging-flow/settings/branches) で `develop`, `staging` ブランチを保護しているのでブランチの削除はできません
1. ここで `production` ブランチが **デプロイ** されるイメージ
1. リリースされたバージョンを github 上でリリース作業を行う
    * [Release 一番最初のリリース · hisasann/git-staging-flow](https://github.com/hisasann/git-staging-flow/releases/tag/v0.0.1)

## 🍫 QA でバグが発生したので直す

QA は `staging` ブランチで行っている前提です

develop ブランチ -> fix ブランチ -> develop ブランチ -> staging ブランチ

1. github で **issue** を作成する
    * [stagingでほげふが画面が表示されない · Issue #5 · hisasann/git-staging-flow](https://github.com/hisasann/git-staging-flow/issues/5)
1. `develop` ブランチから `fix/first` ブランチを作成する
1. `fix/first` で作業をし **commit** する
1. 作業が完了したらローカルの `fix/first` ブランチを、リモートに **push** する
1. github.com のリポジトリページに行きプルリクエストを作成する
    * into `develop` from `fix/first`
1. プルリクエストのレビューを **Reviewers** から受ける
1. **Reviewers** が **approved** する
1. プルリクエストをマージする
1. ここで `develop` ブランチが **デプロイ** されるイメージ
1. `fix/first` ブランチを delete する
1. ここから先は [QA やお客さん確認のためのフロー](https://github.com/hisasann/git-staging-flow#-qa-%E3%82%84%E3%81%8A%E5%AE%A2%E3%81%95%E3%82%93%E7%A2%BA%E8%AA%8D%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AE%E3%83%95%E3%83%AD%E3%83%BC) を参照

## 🍖 本番でバグが発生したので直す

production ブランチ -> develop-* ブランチ -> hotfix ブランチ -> develop-* ブランチ -> staging-* ブランチ -> production ブランチ

1. github で **issue** を作成する
1. `production` ブランチから `develop-hotfix-XXX` ブランチを作成する
1. ローカルの `develop-hotfix-XXX` ブランチを、リモートに **push** する
1. ここで `develop-hotfix-XXX` ブランチが **デプロイ** されるイメージ

`develop-hotfix-XXX` ブランチとしてるのは、 `develop` ブランチがすでに新規開発で **commit** が進んでいると想定した場合の命名です

一時的に `develop` サーバーは、 `develop-hotfix-XXX` ブランチがデプロイされる想定です

1. `develop` サーバーで本番のバグが発生するかを確認する
1. 再現した場合、 `develop-hotfix-XXX` ブランチから `hotfix/first` ブランチを作成する
1. `hotfix/first` で作業をし **commit** する
1. 作業が完了したらローカルの `hotfix/first` ブランチを、リモートに **push** する
1. github.com のリポジトリページに行きプルリクエストを作成する
    * into `develop-hotfix-XXX` from `hotfix/first`
1. プルリクエストのレビューを **Reviewers** から受ける
1. **Reviewers** が **approved** する
1. プルリクエストをマージする
1. ここで `develop-hotfix-XXX` ブランチが **再度デプロイ** されるイメージ
1. `hotfix/first` ブランチを delete する
1. ここまできたら QA する [QA やお客さん確認のためのフロー](https://github.com/hisasann/git-staging-flow#-qa-%E3%82%84%E3%81%8A%E5%AE%A2%E3%81%95%E3%82%93%E7%A2%BA%E8%AA%8D%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AE%E3%83%95%E3%83%AD%E3%83%BC) を参照
1. QA が通ったら本番へ [本番へのデプロイフロー](https://github.com/hisasann/git-staging-flow#-%E6%9C%AC%E7%95%AA%E3%81%B8%E3%81%AE%E3%83%87%E3%83%97%E3%83%AD%E3%82%A4%E3%83%95%E3%83%AD%E3%83%BC)
