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
├── doc/                    ← ドキュメント（ガイド・レビュー・手順書）
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

- すべてのドキュメントは `doc/materials/` 配下に置く（詳細は `doc/RULE.md`）

### ファイル命名規則

命名は `doc/rules/md-rule.md` に従う。ベース名は小文字 ASCII のケバブケースとし、AI が作成して人間が確認する文書には `.hm.md` を付ける。

| 種類 | 命名パターン | 例 |
|---|---|---|
| 解説ガイド | `{topic}-guide.hm.md` | `auth-guide.hm.md` |
| レビュー | `review-phase{N}-{topic}.hm.md` | `review-phase3-auth.hm.md` |
| 手順書 | `phase{N}-{topic}-steps.hm.md` | `phase4-route-guard-steps.hm.md` |

### メタデータ

- 各ドキュメントの先頭に `doc/rules/md-rule.md` の front matter を付ける
- バージョンは H1 ではなく front matter の `version` で管理し、更新時にインクリメントする

## ドキュメント更新時の手順

1. `doc/materials/` 配下の md ファイルを編集する
2. front matter の `version` と `date` を更新する
3. 関連する INDEX.md があれば更新する

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
