# 🥭 git-staging-flow

## 🍗 メインとなるブランチたち

### develop

開発中用

### staging

QA や、お客さん確認など、開発者以外の方用

### production

本番用

## 🍜 作っては削除されるブランチたち

### feature/*

新機能の実装で `develop` ブランチから作成されます

### fix/*

QA でバグがあった場合で `develop` ブランチから作成されます

### hotfix/*

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
1. ここで `develop` ブランチへ **デプロイ** がされるイメージ
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
1. ここで `staging` ブランチへ **デプロイ** がされるイメージ
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
1. ここで `production` ブランチへ **デプロイ** がされるイメージ
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
1. ここで `develop` ブランチへ **デプロイ** がされるイメージ
1. `fix/first` ブランチを delete する
