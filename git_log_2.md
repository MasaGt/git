### git logの便利な引数

1. [ツリー表示(--graph)](#sec1)
2. [mergeコミットのみ表示させたい](#sec2)
3. [コミットメッセージにgrepをかけたい](#sec3)
4. [日時による検索](#sec4)
5. [コミッター名やメールアドレスによる検索](#sec5)
6. [とあるブランチのログのみを表示したい](#sec6)

---
<a id="sec1"></a>

### ログをツリー表示させたい

```bash
git log --graph
```
*-a(--all)をつけないと、現在のブランチのみ表示されるので直線で表示される。  
*--onelineをつけないと、一画面に入りきらないことが多い。

---
<a id="sec2"></a>

### mergeコミットのみ表示させたい

```bash
git log --merges
```

---
<a id="sec3"></a>

### コミットメッセージにgrepをかけたい

```bash
git log --grep=<パターン>
```

---
<a id="sec4"></a>

### 日時による検索

~~日以降で検索する場合
```bash
git log -since=<mm/dd/yyyy>
```

<br>

~~日以前で検索する場合
```bash
git log --until=<mm/dd/yyyy>
```

---
<a id="sec5"></a>

### コミッター名やメールアドレスによる検索

```bash
git log --author=<コミッター名/メールアドレス>
```
*著者の一覧を取得したいなら <font color=red>git shortlog -e</font> を使うのが便利

---
<a id="sec6"></a>

### とあるブランチのログのみを表示したい

```bash
git log <ブランチ名>
```
*指定したブランチの全ての履歴を表示するので,--allスイッチは使わなくていい  
*複数のブランチを渡してもいい

