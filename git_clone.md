### clone

- ほかのgitリポジトリをローカルにコピーする

```bash
git clone <source> <destination_dir>
```
*sourceはpathだったり、URLだったりする  
*destination_dirを省略すると、現在のディレクトリにコピーされる

---

### ブランチを指定してcloneする　

- 普通のcloneコマンドは、リモートがチェックアウトしているブランチをチェックアウトする

- ここでは、クローンしたリポジトリでチェックアウトしたいブランチを指定する

```bash
git clone -b <対象ブランチ> <source> <destination_dir>
```

---

### コピーと何が違うの?

- 同じディレクトリを作るのなら、リモートリポジトリをコピペすれば良いのでは？

    ->　コピペではリモート追跡ブランチは存在しない  
    -> そのため、リモートへのpull/pushができない

---

### cloneしてbare repositoryを作成する

```bash
git clone --bare <source> <destination>
```

---

 ### リモートリポジトリのラベルを設定する

 - デフォルトではorigin

 ```bash
 git clone --origin <ラベル名> <source> <destination>

# もしくは
git clone -o <ラベル名> <source> <destination>
 ```

 リモートリポジトリのラベル名については[こちら参照](./remote_repository.md)