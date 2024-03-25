# 目次

1. [pushとは](#sec1)
2. [pushする](#sec2)
3. [git pushだけだと何をpushするのか](#sec3)
4. [リモートにブランチを追加したい](#sec4)
5. [リモートのブランチを削除したい](#sec5)
6. [リモートにタグを追加したい](#sec6)
7. [リモートのタグを削除したい](#sec7)
8. [non bareリポジトリへのpush](#sec8)
9. [全てのブランチの変更を一度でpushする](#sec9)

---
<a id="sec1"></a>

### pushとは

- リモートリポジトリに変更を反映させるコマンド
- リモートリポジトリのブランチやタグの作成/削除もpushで行う

---
<a id="sec2"></a>

### 変更をpushする

```bash
git push <リモートリポジトリのラベル名> <プッシュするブランチ>
```

実は上記コマンドは下記のショートハンドラ

```bash
git push <リモートタグ>　<ローカルブランチ>:<リモートブランチ>
```

---
<a id="sec3"></a>

### git pushだけだと何をpushするのか

```bash
git push
```
*これは現在チェックアウトしているローカルブランチの変更をpushする  
*ほかのブランチの変更はpushされない


---
<a id="sec4"></a>

### 新しく作成したブランチをpushする

- git pushだけでpushできるのは、ローカルのブランチがリモートブランチを追跡できてる時

- 新しいブランチをローカルで作成し、それをリモートにpushするときは "git push" ではできない

- ブランチ名を指定してpushするか、-uオプションを使う

```bash
# 新しいブランチをローカルで作成
git branch <ブランチ名>

# ローカルで作成したブランチをリモートにpush
# 方法1
git push <リモートrepo名> <ブランチ名>

# 方法2
git push -u <リモートrepo名> <ブランチ名>
# -u は --set-upstream の省略
```
*以降はgit pushだけでそのブランチの変更をpushできる

---
<a id="sec5"></a>

### ブランチの削除をpushする

2つの方法がある
1. <ローカルブランチ>:<リモートブランチ>のローカルブランチ部分を空白にする

2.　push --delete(-d) オプションを使う 

<br>

方法1
```bash
# リモートのブランチを削除する
git push <リモートrepo名> :<削除したいリモートブランチ>
*<リモートrepo名>と:の間に半角スペースが入っていること

# ローカル側でも削除する(必要があれば)
git branch -d <削除したいローカルブランチ>
```
*pushでは[リモートのブランチ　+ ローカルの追跡ブランチ]を削除しているだけなので、ローカルにはまだブランチが残っている

<br>

方法2
```bash
# リモートのブランチを削除する
git push --delete <リモートrepo名> <削除したいリモートブランチ>

# ローカル側でも削除する(必要があれば)
git branch -d <削除したいローカルブランチ>
```

---
<a id="sec6"></a>

### タグのpush

- タグの作成後 git push してもタグはpushされない

```bash
git push <リモートrepo> <pushしたいtag名>
```

<br>

- 全てのタグをpushしたい場合

```bash
git push --tags
```

---
<a id="sec7"></a>

### タグの削除をpush

- タグの削除のpushはブランチの削除のpushと同じ

```bash
# リモートのタグの削除
# 方法1
git push <リモートrepo> :<削除したいリモートのタグ名>

# 方法2
git push --delete <リモートrepo> <削除したいリモートのタグ名>

# 残ったローカルのタグの削除
tag -d <削除したいローカルのタグ名>
```

---
<a id="sec8"></a>

### non bareリポジトリへのpushはエラーになる

- リモート側の git config (--local) の receive.denyCurrentBranch にignoreを設定する

*そもそもノンベアリポジトリへのpushは推奨されていないので多用するべきではない

```bash
git config receive.denyCurrentBranch ignore
```

---
<a id="sec9"></a>

### 全てのブランチの変更を一度でpushする

```bash
git push --all
```