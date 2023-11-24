### git stashとは

- ワーキングディレクトリの変更を一時的に退避するコマンド

---

### 現在の変更を退避する

```bash
git stash
```
*untracked なファイルは退避されない

---

### 現在の変更を退避する　　
*untrackedなファイルも退避する

```bash
git stash -u
```

---

### stashの指定の仕方
```bash
stash@{n}
```

---

### 退避した変更を取り出し、リストから削除する　

```bash
git stash pop (対象stash)
```
*対象stashを指定しないと、一番新しいstashがpopされる

---

### 退避した変更を取り出し、リストには残す

```bash
git stash apply (対象stash)
```
*対象stashを指定しないと、一番新しいstashがapplyされる

---

### 退避しているstashを削除する

```bash
git stash drop (対象stash)
```
*対象stashを指定しないと、一番新しいstashがdropされる

---

### 退避している変更を全て削除する

```bash
git stash clear
```

---

### stashにコメントをつける
```bash
git stash save "コメント"
```
*これで、pop/apply/drop <対象stash>の対象stashはコメントでも指定できるようになる


---

### 退避した変更の一覧

```bash
git stash list
```

---

### 

---

### 違うブランチでpopするとconflictが起こる時がある

- 解決手順
    1. git reset (git restore --staged) <対象ファイル>  
    -> コンフリクトが起きているファイルをアンステージングする

    2. git restore  
    -> ワーキングディレクトリの変更を破棄する
    
    3. git checkout <ブランチ名>  
    -> 正しいブランチに戻る
    
    4. git stash pop  
    -> 退避しておいた内容を取り出す

