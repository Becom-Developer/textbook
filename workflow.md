# WORKFLOW

開発の進め方について

```text
案件の開発が少人数(1人~3人程度)を想定して過去に実施していた
特にこだわりがない場合はこのやり方を参考にしたい。
```

- [STEP1](#step1) 課題管理
- [STEP2](#step2) 実装作業
- [STEP3](#step3) レビュー
- [STEP4](#step4) 公開

## STEP1

課題管理

github の prject 機能を活用したい

- <https://docs.github.com/ja/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects>

## STEP2

実装作業

git のブランチごとに進める

1. issue ごとにブランチを作成する
1. issue が完了時に作業ブランチをレビュー main ブランチへ取り込み
1. issue クローズ時に作業ブランチも破棄する

手順

手元のPCから github の Pull requests に登録依頼をだす

- 正常に git clone が完了している前提
- イシューごとにブランチを作成
- 例: イシューのタイトルが 「開発環境構築 #1」 の場合

```console
git fetch origin && \
git checkout -b dev#1 origin/main && \
git commit -m 'pullreq commit' --allow-empty && \
git push origin dev#1
```

github へアクセスし pull requests を作成する

pull requests 作成後は手元のソースコードを更新するたびにこまめにプッシュする

- コミットからプッシュまでのコマンド(MEMO のところは任意のメッセージ)

```console
git add .
git commitn -m 'MEMO'
git push origin dev#1
```

## STEP3

レビュー

コードをレビューして main ブランチに反映する人

- レビュー担当者の端末にて開発ブランチを確認

```console
git checkout dev#1
```

- 最新の main ブランチを取り込んでコンフリクトなどがおこらないか確認

```console
git merge -m 'origin main' origin/main
```

- レビュー後問題なければ最新の開発ブランチをリモートブランチに送信

```console
git push origin dev#1
```

## STEP4

公開

- github の pull requests の画面上で `Merge pull request` ボタンを使い main ブランチと統合
- main ブランチに取り込んだ後はブランチを削除しておく
- 手元のローカルブランチを削除するのは下記のコマンド

```console
git branch -d dev#1
```

最近は github の main ブランチを更新すると自動的に公開環境へデプロイするツールなどもあるので必要に応じて活用
