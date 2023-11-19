### git reset

- コミットの取り消しを行う

- ステージングされた変更を取り消す

---

### git restore

- ステージングされた変更を取り消す

- ワーキングディレクトリの変更を取り消す

---

### 共通点と相違点

- 共通点
    - ステージングされた変更を取り消す

- 相違点
    - resetは主にコミット履歴への変更を行う

    - restoreはワーキングディレクトリとステージングの変更のみを取り消せる

---

### git resetの使い方

ステージングされた変更の取り消し

- git reset <ファイル名>

```bash
# 間違って変更途中のファイルをgit add してしまった
git add sample.txt

# ステージングエリアにaddしたファイルを取り消す
git reset sample.txt
```

<br>

コミットの取り消し

TODO: コミットの取り消し操作を追加する

---

### git restoreの使い方

ステージングされた変更の取り消し

- git restore --staged <ファイル名>

```bash
# 間違って変更途中のファイルをgit add してしまった
git add sample.txt

# ステージングエリアにaddしたファイルを取り消す
git restore --staged sample.txt

```

<br>

ワーキングディレクトリの変更の取り消し

- git restore <ファイル名>

```bash
# sample.txtに変更を加えたが、やっぱり元に戻したい
git restore sample.txt
```