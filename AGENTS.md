# Service Template

このリポジトリは新サービスのひな形です。

## Submodules

このリポジトリはgit submoduleを使っています。

### セットアップ
```bash
git clone --recursive <this-repo>
# または clone後に
git submodule update --init --recursive
```

### submodule更新
```bash
git submodule update --remote
```

### infraの差し替え（インフラ変更時）
```bash
git submodule set-url infra <new-infra-repo-url>
git submodule update --remote
```

## 構成

- `app/` — サービス本体のコード
- `common/` — 共通contracts・ヘルパー（pipeline-common）
- `infra/` — インフラwiring（k12-network-notes）

## 新サービス作成手順

1. このリポをclone（--recursive）
2. `app/` をサービス名に合わせて編集
3. `common/` はそのまま使用（JobResult, ArtifactStore等）
4. `infra/` の中のwiring定義をコピー・編集してサービス固有のwiring追加
