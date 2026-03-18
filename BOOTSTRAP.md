# Bootstrap

このファイルが存在する = 未セットアップ。
セットアップ完了後にこのファイルを削除すること。

## 手順

### 1. サービス名を設定

`service.config.yaml` を作成：

```yaml
service_name: <サービス名をここに記入>
infra:
  url: <infraリポのGitHub URL（例: https://github.com/ishii2025buziness/k12-network-notes）>
  type: k12  # k12 or other
```

### 2. infra submoduleを追加

```bash
git submodule add <infra.url> infra
git submodule update --init --recursive
```

### 3. app/pyproject.tomlのservice_nameを更新

`app/pyproject.toml` の `name = "service-name"` を実際のサービス名に変更。

### 4. app/src/pipeline.py のpipeline名を更新

`pipeline="service-name"` を実際のサービス名に変更。

### 5. このファイルを削除

```bash
git rm BOOTSTRAP.md
git commit -m "bootstrap: initialize <サービス名>"
```
