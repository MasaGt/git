### リポジトリにコミットしたファイルの名前や、ディレクトリを変更したい場合

1. mv　で対象ファイル削除
2. git mv で対象ファイル削除

- mvコマンドでファイルを削除した場合

    1. mvで対象ファイル名変更
    2. git rm (対象ファイル) でリネーム前のファイルを削除したことをステージングエリアにあげる
    3. git add (対象ファイル) でのリネーム後のファイルを追加したことをステージングエリアにあげる
    3. git commit でリネームしたということをコミットする


- git mv コマンドでファイルを削除した場合

    1. git mv (対象ファイル) で対象ファイルのリネーム&ステージングエリアに反映
    2. git commit でリネームしたということをコミットする

つまり、git mv コマンドを利用すると、mvでの手順2,3を省略できる

---

### 利用例

事前準備
```bash
# いくつかファイルを作成して、コミットしておく
touch a b
git add .
git commit -m "first commit"
```

mvコマンドの例
```bash
# aファイルをrenamedにリネーム
mv a renamed

# aファイルを削除したということをステージングする
git rm a # もしくは git add a

# renamedを追加したということをステージングする
git add renamed

# 上記コマンドを完了すると、git側で a -> renamed　でリネームされたと理解する

# aファイルをrenamedにリネームしたことをコミットする
git commit (renamed -m "chage file name from a to renamed")
```

git mvコマンドの例
```bash
# bファイルをanother_renameにリネーム
git mv b another_rename

# すでにbファイルを削除したこと+another_renameを追加したことはステージングされている
# つまりb -> another_renameにリネームしたことはステージングされている
# よってコミットする
git commit (another_rename -m "change file name from b to another_rename")
```