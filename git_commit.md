### 一番最初のコミットはからコミットにするべき

--- 

### git add　と git commit を一度で行なってしまう

- git commit -a　もしくは git commit --all で行うことができる

- 注意点: 対象ファイルは一度コミット済みであること

```bash
# 一度対象ファイルはコミット済みであること
git commit -a (対象ファイル) (-m "comment")
# もしくは
git commit --all (対象ファイル) (-m "comment")
```
---

### commit は複数のファイルのうち、選択してcommitできる

```bash
# 複数ファイルを作成し、全てaddする
touch a b c d
git add .

# addされた a と b のみをコミットしたい場合
git commit a b (-m "comment")
```