<a id="sec1"></a>

### pullとは

- ほかのリポジトリの変更を取り込むコマンド

- git pull = (git fetch) + (git merge)

---
<a id="sec2"></a>

### pullする

```bash
git pull
```

実は上記コマンドは下記のショートハンドラ

```bash
git pull <リモートリポジトリのラベル名> <プルするリモートのブランチ名>
```

---

### pullをfast forwardに限定する

- fast forward マージが可能なpullしか実行しない

```bash
git pull --ff-only
```
*もし、コンフリクトが起きるpullのときはfetchも実行されない

<br>

git configにも設定できる

```bash
git config pul.ff only
```

---

### pullでコンフリクトが起きたら

方法1

1. コンフリクトを解決し、ローカルリポジトリにコミット
2. コンフリクトを解決したコミットをリモートリポジトリにpush


