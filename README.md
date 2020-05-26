# git-staging-flow

## メインとなるブランチたち

### develop

開発中用

### staging

QA や、お客さん確認など、開発者以外の方用

### production

本番用

## 開発をするときのフロー

1. `develop` ブランチから `feature/first` ブランチを作成する
1. `feature/first` で作業をし **commit** する
1. 作業が完了したらローカルの `feature/first` ブランチを、リモートに **push** する
1. github.com のリポジトリページに行きプルリクエストを作成する
    * `develop` from `feature/first`
1. プルリクエストのレビューを **Reviewers** から受ける
1. **Reviewers** が **approved** する
1. プルリクエストをマージする
1. `feature/first` ブランチを delete する
