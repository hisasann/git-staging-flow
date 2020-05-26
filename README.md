# git-staging-flow

## メインとなるブランチたち

### develop

開発中用

### staging

QA や、お客さん確認など、開発者以外の方用

### production

本番用

## 開発をするときのフロー - develop ブランチ

1. `develop` ブランチから `feature/first` ブランチを作成する
1. `feature/first` で作業をし **commit** する
1. 作業が完了したらローカルの `feature/first` ブランチを、リモートに **push** する
1. github.com のリポジトリページに行きプルリクエストを作成する
    * `develop` from `feature/first`
1. プルリクエストのレビューを **Reviewers** から受ける
1. **Reviewers** が **approved** する
1. プルリクエストをマージする
1. `feature/first` ブランチを delete する

```
*   d87f0c9 (origin/develop) Merge pull request #1 from hisasann/feature/first
|\
| * 361dd3f (origin/feature/first, feature/first) first commit to feature/first
|/
* a34f262 (origin/staging, origin/production, staging, production) first commit
```

## QA やお客さん確認のためのフロー - staging ブランチ

1. github 上で **New pull request** をクリックする
1. base: `staging` ブランチ <- `develop` ブランチを選択する
1. タイトルやコメントを書く
1. **Create pull request** をクリックする
1. **Merge pull request** をクリックする
1. **Confirm merge** をクリックする
1. [Branches](https://github.com/hisasann/git-staging-flow/settings/branches) で `develop`, `staging` ブランチを保護しているのでブランチの削除はできません









