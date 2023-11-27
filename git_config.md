# 目次

1. [git configコマンドとは](#sec1)

2. [gitconfigのレベル](#sec2)

3. [各レベルの設定ファイルの場所](#sec3)

4. [優先順位](#sec4)

5. [gitconfigの読み取り](#sec5)

6. [gitconfigへの書き込み](#sec6)

7. [設定項目の削除](#sec7)

8. [よくある設定項目](#sec8)

9. [項目をgrepする](#sec9)

<br>

---
<a id=sec1></a>

### git configコマンドとは


Gitの設定ファイル(gitconfig)にアクセスし、書き込み/読み取りを行うコマンド

---
<a id=sec2></a>

### gitconfigのレベル

Gitの設定には3段階ある

1. System level: そのマシンの全ユーザーに適応される設定 

2. Gobal level: そのユーザーのみに適応される設定

3. Local level: そのリポジトリ(フォルダ)のみに適応される設定

---
<a id=sec3></a>

### 各レベルの設定ファイルの場所

1. System level: 
```
[Mac]
主に以下のどっちか
/usr/local/etc/gitconfig
/usr/local/git/etc/gitconfig

homebrewでgitをインストールした場合は以下
/opt/homebrew/etc

[Windows]
C:¥Program Files¥Git¥etc¥gitconfig
```


2. Global level:
```
[Mac]
~/.gitconfig

[Windows]
C:¥Users¥[ユーザー名]¥.gitconfig
```

3. Local level:
```
[Mac & Windows]
[リポジトリのルートディレクトリ]/.git/config
```

---
<a id=sec4></a>

### 優先順位

優先順位は、system < global < local 

これはファイルの読み込み順が system -> global -> local で後から読んだ値がその前の値を上書くから

---
<a id=sec5></a>

### gitconfigの読み取り

```bash
git config [レベル] <設定項目名>

# 例: グローバルレベルのユーザー名を読み取る
git config --global user.name
```

<br>

```bash
# 設定されているすべての項目を表示する
git config [レベル] -l
git config [レベル] --list

# 例: ローカルレベルで設定されている項目を表示する
git config --local -l
# 例: 全てのレベルで設定されている項目を表示する
git config -l
```

<br>

全レベルで表示するが、各項目がどのレベルの設定項目なのかを確認したい場合

```bash
git config -l --show-origin
# git config --show-origin -l でも可
```

---
<a id=sec6></a>

### gitconfigへの書き込み

```bash
git config [レベル] <設定項目名> <設定値>

# 例: グローバルレベルのユーザー名を設定する
git config --global user.name hogehoge
```
*設定のレベルを省略すると、デフォルトで Local level のgitconfigに書き込まれる

<br>

```bash
# 設定ファイルをエディタで直接編集
git config [レベル] -e
```

---
<a id=sec7></a>

### 設定項目の削除

```bash
git config [レベル] --unset <設定項目>

# 例: グローバルレベルのユーザー名を削除する
git config --global --unset user.name
```

---
<a id=sec8></a>

### よくある設定項目

1. デフォルトのブランチ名
```bash
git config --global init.defaultBranch <設定値>
```
<br>

*これに付随するよくある問題  
[条件] GitHubでは、現在デフォルトのブランチ名はmain  
自分のマシンではデフォルトのブランチ名はmasterに設定してあった  

↓  

[問題]自分のコミットをGitHubのリポジトリへpushしようとしたらエラー発生

[解決策]自分のマシンで作業する前に、デフォルトで作成されるブランチ名を確認し、設定されていなければmainと設定する

<br>

2. ユーザー名&メールアドレス

```bash
git config --global user.name <ユーザー名>
git config --global user.email <メールアドレス>
```
* 両項目とも設定値を""で囲む

<br>

3. pushするときのdefaultブランチを設定
```bash
git config --global push.default <設定値>

# pushする際デフォルトブランチを現在いるブランチにする
git config --global push.default current
```
*これを設定していないと、pushしたときにリモートブランチを指定しろと怒られる時がある

---
<a id=sec9></a>

### git configの項目をgrepする

- パターンに一致した項目のみ表示する

```bash
git config --get-regexp <パターン>
```
