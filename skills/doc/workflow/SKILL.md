---
name: doc-workflow
description: ドキュメント運用と開発ワークフローのテンプレート。
license: Proprietary
compatibility: opencode
metadata:
  domain: doc
  audience: project
  output: guidance
---

## What I do

プロジェクトにおけるドキュメント運用フローと開発ワークフローを定義します。

## プロジェクト構成

```
<project-root>/
├── docs/                   ← ドキュメント（ガイド・レビュー・手順書）
├── <app-source>/           ← アプリケーションのソースコード
│   ├── src/
│   │   ├── proxy.ts        ← ルーティング/保護レイヤー
│   │   ├── lib/
│   │   └── db/
│   ├── docker-compose.yml
│   └── package.json
└── demo/
```

## ドキュメント規約

### 配置場所

- すべてのドキュメントは `docs/` ディレクトリに置く

### ファイル命名規則

| 種類 | 命名パターン | 例 |
|---|---|---|
| 解説ガイド | `{topic}_guide.md` | `auth_guide.md` |
| レビュー | `review_phase{N}_{topic}.md` | `review_phase3_auth.md` |
| 手順書 | `phase{N}_{topic}_steps.md` | `phase4_route_guard_steps.md` |

### バージョン番号

- 各ドキュメントの h1 末尾にバージョン番号 `[#N]` を付ける
- 内容を更新したらインクリメントする

## ドキュメント更新時の手順

1. `docs/` 配下の md ファイルを編集する
2. h1 のバージョン番号をインクリメントする
3. 関連する INDEX.md があれば更新する
4. プレビューサーバーで表示を確認する（`bash docs/serve.sh`）

## コーディング規約

### 命名
- アプリ層は可読性重視（例: キャメルケース）
- 永続層は対象 DB/ORM の規約に合わせる（例: スネークケース）

### セッション/トークン受け渡し
- 方式（クエリ、Cookie、Header）はプロジェクト要件で統一する

### 回答言語
- 日本語で回答する

## 例外

### ドキュメント追記を行わないケース
- ユーザーが「チャットでいい」と明示した場合は、ドキュメント更新を行わない
