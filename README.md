# jujutsu_memo

## セットアップ

```zsh
brew install jj
```

Git と同様にメールアドレスとユーザー名を設定する

```zsh
jj config set --user user.name "ユーザー名"
jj config set --user user.email "メールアドレス"
```

## GitHub リポジトリをクローンする

```zsh
jj git clone https://github.com/HiroyukiIsoe/jujutsu_memo.git

Fetching into new repo in "（ディレクトリ）/workspace/jujutsu_memo"
Working copy now at: qvzzqoso d092fc40 (empty) (no description set)
Parent commit      : lrosmkmt 2db69ab3 main | Initial commit
Added 1 files, modified 0 files, removed 0 files
```

## コマンドラインでのオートコンプリートを有効化する

### Zsh

```zsh
autoload -U compinit
compinit
source <(jj util completion --zsh)
```

## デフォルトエディターの設定

```zsh
jj config edit --repo
```

`.jj/repo/config.toml`ファイルが作成されるので、エディター設定を追記する

```text
ui.editor = "vim"
```

## 変更情報の作成

```zsh
jj describe
```

vim が起動するので、コメントを記載する

## 状態の確認

```zsh
jj st

Working copy changes:
M README.md
Working copy : qvzzqoso 63ba8568 セットアップ方法の追記
Parent commit: lrosmkmt 2db69ab3 main | Initial commit
```

## 差分の確認

````zsh
jj diff --git

diff --git a/README.md b/README.md
index 1e5d66ea47...00b31e71e5 100644
diff --git a/README.md b/README.md
index 1e5d66ea47...00b31e71e5 100644
diff --git a/README.md b/README.md
index 1e5d66ea47...00b31e71e5 100644
--- a/README.md
+++ b/README.md
@@ -1,1 +1,66 @@
-# jujutsu_memo
\ No newline at end of file
+# jujutsu_memo
+
+## セットアップ
+
+```zsh
+brew install jj
+```
+
+Git と同様にメールアドレスとユーザー名を設定する
+
+```zsh
+jj config set --user user.name "ユーザー名"
+jj config set --user user.email "メールアドレス"
+```
(省略)
````

## 新しいコミットを作成する

```zsh
jj new
```

```zsh
jj st

The working copy is clean
Working copy : qnqouwvl fcb9679c (empty) (no description set)
Parent commit: qvzzqoso 90a2af3b セットアップ方法の追記
```

## 変更を追加する

```zsh
jj squash
```

## GitHub のリポジトリに変更を Push する

### ブランチ名を指定しない方法

```zsh
# mainブランチから新しい変更を始める
jj new main
# 変更をコミットして記録する
jj commit -m 'hogehoge'
# GitHubへPushする
# ブランチ名は自動で
jj git push -c @-
```

### ブランチ名を指定する方法

```zsh
jj new main

jj commit -m 'hogehoge'
# コミット内容を含むブランチを作成する
$ jj branch create test -r @-
# Push the branch to GitHub (pushes only `bar`)
$ jj git push
```

## GitHub リポジトリの変更を取り込む

```zsh
jj git fetch
jj rebase -d $main_branch
```
