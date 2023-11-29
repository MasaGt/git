#目次

1. [rebaseとは](#sec1)
2. [rebaseの具体的なユースケース](#sec2)
3. [rebase対象のコミットを知る](#sec3)
4. [rebaseの使い方](#sec4)
5. [rebaseを取り消したい場合](#sec5)
6. [コミット履歴の整理(squash)](#sec6)
7. [コミット履歴の整理(squash) ver2](#sec7)
8. [一番最初のコミットもrebaseの対象に含める方法](#sec8)
9. [対話型rebase](#sec9)
10. [rebaseする際にコンフリクトが起きた場合](#sec10)
11. [rebaseのabort](#sec11) 
12. [rebaseのskip](#sec12)

---
<a id="sec1"></a>

### rebaseとは

- 指定したブランチの分岐点を変えるコマンド

<font color=red>リベースされたコミットはコミットIDが変わる</font>
<img src="./img/rebase.jpg" />

[source: git rebaseの具体的なメリット](https://zenn.dev/tana0102/articles/475d8952933af6)

- ローカルのコミット履歴を合成して一つにする(squash)

*<font color=red>プッシュしたコミットをリベースしてはいけない -> コミットIDが変わるから</font>

---
<a id="sec2"></a>

### rebaseの具体的なユースケース

- featureブランチで作業指定していて、masterの新しい変更を取り込みたいとき  
    -> rebaseコマンドでfeatureブランチの分岐点を変更する

- リモートにプッシュする前に、ローカルのコミット履歴を綺麗にしてからプッシュしたい

---
<a id="sec3"></a>

### rebase前にリベースされるコミットを知る

ブランチAにあってブランチBにないコミットを表示する
```bash
git log <ブランチB>..<ブランチA>
```
*イメージとしては、ブランチAとブランチBの共通コミットからブランチAの最新コミットまでを表示する

*ブランチAをブランチBにリベースするとき、上記コマンドで表示されるコミットたちがリベースされるコミット

---
<a id="sec4"></a>

### rebaseする

2つの方法がある  
1. リベースしたいブランチにチェックアウトして分岐点を変更
2. リベースしたいブランチと分岐点を指定(どこのブランチにいても大丈夫)  
*方法2は指定順を間違えると大変なことになる

方法1
```bash
# リベースしたいブランチにチェックアウト
git checkout <リベースしたいブランチ>

git rebase <変更先分岐点>
```
*<font color=red>分岐点はコミットIDだったりブランチ名だったり</font>

方法2
```bash
git rebase <変更先分岐点> <リベースしたいブランチ>
```

---
<a id="sec5"></a>

### rebaseを取り消したい場合

まずはgit reflogでrebase前のHEADの履歴を調べる
```bash
git reflog
```

<img src="./img/rebase_cancel.png" />

<br>
上記コマンドからHEAD@{4}にHEADを戻せばいいとわかる

```bash
git reset --hard HEAD@{4}
```
*--hardはステージングエリア&作業ディレクトリの両方がリセットされる

---
<a id="sec6"></a>

### コミット履歴の整理(squash)

- 現在のブランチの特定のコミット以降のを編集する  

<font color=red>コミットIDの指定が少し奇妙</font>  
->編集したいコミットの一つ前のコミットIDを指定する

例
squashしたいコミットを確認する
<img src="./img/squash1.png" />

<br>

```bash
git rebase -i <squashしたい範囲の一つ前のコミットID> <squashしたい範囲の最後のコミットID>
```
<img src="./img/squash2.png" />

<br>

rebaseの対象が正しく出ているか確認
<img src="./img/squash3.png" />

---
<a id="sec7"></a>

### コミット履歴の整理(squash) ver2.

- もし、一つのコミットIDのみ指定すると、そのコミットの次のコミットから、現在のコミットまでが　squash対象になる

```bash
git rebase -i <対象範囲の一つ前のコミットID>
```

<img src="./img/squash4.png" />

<br>

<img src="./img/squash5.png" />

<br>

<font color=red>そしたら、一番最初のコミットはrebaseできない?</font>  
[->解決策](#sec8)

---
<a id="sec8"></a>

### 一番最初のコミットもrebaseの対象に含める方法

```bash
# 一番最初から一番最後のコミットまでrebaseする場合
git rebase -i --root
```

<img src="./img/squash6.png" />

結果

<img src="./img/squash7.png" />


```bash
# 一番最初から特定のコミットまでrebaseする場合
git rebase -i --root <対象範囲の最後のコミットID>
```

---
<a id="sec9"></a>

### 対話型rebase

- rebaseする際、リベースするコミットたちの編集が行える

例: mainとnewブランチがあり、newブランチをmainの最新コミットにリベースしたい場合
<img src="./img/rebase_i_1.png" />

<br>

rebase -i でリベースする
<img src="./img/rebase_i_2.png" />

<br>

viで各コミットを編集し、newブランチをmainの最新コミットにリベースする
<img src="./img/rebase_i_3.png" />

<br>

リベースされたか確認する
<img src="./img/rebase_i_4.png" />

*リベースされたブランチはpush -fでしかpushできない(そのブランチの親コミットが変わっているかわ)


---
<a id="sec10"></a>

### rebaseする際にコンフリクトが起きた場合

mergeのコンフリクトと違う点

- mergeのコンフリクト  
    merge対象のブランチの全てのコミットファイルのコンフリクトがmergeの際に一気に発生する

このようなリポジトリがあったとして、mainとfeatureをmergeする際にコンフリクトが起きるとしたら
<img src="./img/conflict_merge_rebase.png">

mergeコミットで一気に起きる
<img src="./img/conflict_merge.png" />

<br>

- rebaseのコンフリクト  
    リベース対象のコミットを一つ一つコピーを作成し、リベース先に繋ぐので、一個一個つなぐ際にコンフリクトが起きる

このようなリポジトリがあったとして、mainとfeatureをmergeする際にコンフリクトが起きるとしたら
<img src="./img/conflict_merge_rebase.png" />

<br>

もし、featureブランチのCコミットとmainでコンフリクトがあるならこうなる
<img src="./img/conflict_rebase1.png">

c'のコンフリクトを解決して git add & git rebase --continueする

もし、featureブランチのDコミットとmainでコンフリクトがあるならこうなる
<img src="./img/conflict_rebase2.png" />

---
<a id="sec11"></a>

### rebaseのabort

- rebase時にコンフリクトが発生した際、 git rebase --abrtとすることで、rebaseを取り消す

```bash
git rebase --skip
```

<br>

例: コンフリクトが起きるrebase

mainとnewブランチで同じファイルを変更していた場合
<img src="./img/rebase_abort_skip_base.png" />

<br>

rebase時にコンフリクト発生
<img src="./img/rebase_abort1.png" />

<br>

ログをみるとコンフリクトの起きなかったコミットはrebaseされている
<img src="./img/rebase_abort2.png" />

<br>

git rebase --abort すると、今回のrebaseを全て取り消す
<img src="./img/rebase_abort3.png" />

---
<a id="sec12"></a>

### rebaseのskip

- rebase時にコンフリクトが発生した際、 git rebase --skip とすることで、コンフリクトしたコミットのみを取り消すことができる  
*コンフリクトの起きたコミットのみ --abort できるイメージ

例: コンフリクトが起きるrebase

mainとnewブランチで同じファイルを変更していた場合
<img src="./img/rebase_abort_skip_base.png" />

<br>

rebase時にコンフリクト発生
<img src="./img/rebase_abort1.png" />

<br>

ログをみるとコンフリクトの起きなかったコミットはrebaseされている
<img src="./img/rebase_abort2.png" />

<br>

git rebase --skipすると、コンフリクトの起きたコミットが捨てられる  
*リモート追跡ブランチからもそのコミットが消えている
<img src="./img/rebase_skip_1.png" />

