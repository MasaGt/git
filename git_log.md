### git logの便利な引数

- --stat: 各コミットログを構成しているファイルを表示する

```bash
# バッチファイルを作って、コミットする
touch sample.bat
git add sample.bat
git commit -m

git log --stat

# commit d166767e6082fb746e0fc412ef3994d9cbd75acd (HEAD -> main)
# Author: MasaGt <MasaGt@example.com>
# Date:   Sat Nov 18 13:16:12 2023 +1300

#     create a batch file

#  sample.bat | 0 ★ここにコミットを構成するファイルが表示される
#  1 file changed, 0 insertions(+), 0 deletions(-)
```

---

- --stat: コミットログに、変更されたファイルの情報を表示する


```bash
git log --stat --oneline

# 65d0287 (HEAD -> main) Adding four empty files
# ★ここから
#  a | 0
#  b | 0
#  c | 0
#  d | 0
#  4 files changed, 0 insertions(+), 0 deletions(-)
# ★ここまで
# c02f470 add b variable
# ★ここから
#  math.sh | 1 +
#  1 file changed, 1 insertion(+)
# ★ここまで
# d4e7241 This is the second commit
# ★ここから
#  math.sh | 1 +
#  1 file changed, 1 insertion(+)
# ★ここまで
# 8eb1ed3 This is the first commit
# ★ここから
#  math.sh | 1 +
#  1 file changed, 1 insertion(+)
# ★ここまで
```

---

- --shortstat: --stat コマンドのうち、変更/追加/削除 の行だけを表示する

```bash
git log --shortstat --oneline

# 65d0287 (HEAD -> main) Adding four empty files
#  4 files changed, 0 insertions(+), 0 deletions(-)　★ここ
# c02f470 add b variable
#  1 file changed, 1 insertion(+) ★ここ
# d4e7241 This is the second commit
#  1 file changed, 1 insertion(+) ★ここ
# 8eb1ed3 This is the first commit
```

