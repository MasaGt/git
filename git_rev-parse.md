- コミットのハッシュ値を取得できる

```bash
# HEADのハッシュ値を取得できる　
git rev-parse HEAD

# mainブランチの最新コミットのハッシュ値を取得
git rev-parse main
```

### オプション

- --short: 省略されたコミットのハッシュ値を表示する

```bash
# HEADのハッシュ値(省略した形)を取得できる　
git rev-parse --short HEAD

# sampleブランチの最新コミットのハッシュ値(省略形)を取得
git rev-parse --short sample
```