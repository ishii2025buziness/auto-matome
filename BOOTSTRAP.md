# Bootstrap

このファイルが存在する = 未セットアップ。
セットアップ完了後にこのファイルを削除すること。

## ヒアリング方法

ユーザーへの質問はインタラクティブなツールを使うこと：

- **Claude Code** — `AskUserQuestion` ツールを使う（選択肢を提示してユーザーが選べる）
- **その他のエージェント** — 同等のインタラクティブUIツールがあれば使う。なければ1問ずつ質問して回答を待つ

## 手順

### 1. サービス名を設定

`service.config.yaml` を作成：

```yaml
service_name: <サービス名をここに記入>
artifact_root: .artifacts
infra:
  url: https://github.com/ishii2025buziness/k12-network-notes  # デフォルト。変える場合はここを書き換える
  type: k12
```

### 2. infra参照を clone する

デフォルト（k12-network-notes）の場合：

```bash
git clone https://github.com/ishii2025buziness/k12-network-notes infra
```

別のインフラを使う場合は `service.config.yaml` の `infra.url` を変更してから上記コマンドのURLを差し替える。

これは deploy 先インフラを近くで参照するための clone であり、編集の正本を service repo に持つためではない。
host wiring の変更が必要なら、infra 本体 repo 側で commit / review すること。

### 3. infraのデータパスを確認する

`infra/` のマウント定義を読み、コンテナの `/data` がホストのどこにマウントされるかを確認する。
`service.config.yaml` の `artifact_root` をそのパスに合わせること。

確認先の目安:

- `infra/nixos/modules/` の service module
- `infra/nixos/hosts/` の host import / enable
- `infra/containers/` の compose, Containerfile, systemd 関連ファイル

### 4. app/pyproject.tomlのservice_nameを更新

`app/pyproject.toml` の `name = "service-name"` を実際のサービス名に変更。

### 5. app/src/pipeline.py の job 名を更新

`service-name` のダミー値を実際のサービス名に変更。

### 6. このファイルを削除

```bash
git rm BOOTSTRAP.md
git commit -m "bootstrap: initialize <サービス名>"
```
