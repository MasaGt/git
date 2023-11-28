### エイリアスの設定方法

- 設定ファイル(.gitconfig)にエイリアスを書き込む

[.gitconfigに設定を追加する方法](./git_config.md#sec6)

---

### エイリアスの設定

```bash
git config <レベル> alias.<エイリアス> "<実際のコマンド>"
```

例: git status を git ss で実行したい
```bash
git config alias.ss "status"
```

log --all --oneline --graph