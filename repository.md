### repositoryとは

- ファイルやディレクトリの変更を記録/管理する場所のこと
- 正体は.gitディレクトリ

---

### bare reposioryとは

- 作業ディレクトリを持たないrepositoryのこと
- このリポジトリでは作業ができない(git add/statusなど実行できない)
- このリポジトリは更新情報を持つ(ほかのリポジトリからpushされたりpullされたり)
- bare repository名は~~~.gitになるのが慣例
- リモート追跡ブランチを持たない  
    ->リモートリポジトリとなることが多い

---

### bare repositoryの作成

```bash
git init --bare
```

---

### クローンするが、そのリポジトリをbare repositoryにする

```bash
git clone --bare <source> <destination>
```
