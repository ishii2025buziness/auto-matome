# Service Template

新サービスのひな形リポジトリ。

## 初回セットアップ

**BOOTSTRAP.mdが存在する場合、必ず最初にそれに従うこと。**

BOOTSTRAP.mdがない = セットアップ済み。

## 新サービスの作り方

```bash
gh repo create <service-name> --template ishii2025buziness/service-template --public --clone
cd <service-name>
git submodule update --init --recursive  # common submoduleを初期化
```

その後BOOTSTRAP.mdに従う。

## Submodules

- `common/` → [pipeline-common](https://github.com/ishii2025buziness/pipeline-common)（共通contracts・ヘルパー）
- `infra/` → bootstrap時に設定するインフラリポ

### submodule操作

```bash
# common更新
git submodule update --remote common

# infra更新
git submodule update --remote infra
```

## 構成

- `app/` — サービス本体（run/smoke/check CLI）
- `common/` — 共通ライブラリ（JobResult, ArtifactStore等）
- `container/` — Containerfile・entrypoint.shひな形
- `infra/` — インフラwiring（bootstrap後に設定）
- `docs/` — 設計・契約ドキュメント
- `skills/` — サービス固有スキル
- `progress/current.md` — 進捗・ハンドオフ
- `service.config.yaml` — サービス設定（bootstrap後に生成）

## ドキュメント

- `docs/contracts.md` — **実装時に必ず確認すること**。強制する契約と独自でよい部分を定義。
