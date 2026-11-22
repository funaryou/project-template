---
name: doc-architecture
description: プロジェクトのドキュメント配置思想、構造、管理ルールを定義する。
license: Proprietary
compatibility: opencode
metadata:
  domain: doc
  audience: project
  output: guidance
---

## What I do

プロジェクトのドキュメント構造と管理ルールを定義し、迷子ファイルの発生を防ぎます。

## 設計理念

ドキュメントは「生きた資産」であり、コードと同様に整理され、検索可能でなければなりません。開発フェーズ、機能、技術レイヤーごとにディレクトリを分離し、迷子ファイルの発生を防ぎます。

## ドキュメント構造

すべてのドキュメントは `doc/` ディレクトリ配下に、以下の役割別に分類します。

| ディレクトリ | 役割 | 主な内容 |
| :--- | :--- | :--- |
| `database/` | データ設計 | ER図、テーブル定義、マイグレーション手順、スキーマ解説 |
| `features/` | 機能仕様・実装 | 各機能の具体的な仕様と実装記録（`impl_*.md`） |
| `implementation/` | 開発プロセス | 環境構築手順、開発フェーズ別計画書、実装ガイドライン |
| `verification/` | 検証・レビュー | レビュー結果（`review_*.md`）、検証手順書、テスト証跡 |
| `misc/` | その他 | 一時的なメモ、作業予定、雑多な記録 |

## ファイル命名規則

命名は `doc/rules/md-rule.md` に従う。ベース名は小文字 ASCII のケバブケースとし、AI が作成して人間が確認する文書には `.hm.md` を付ける。

| 種類 | 命名パターン | 例 |
| :--- | :--- | :--- |
| 実装記録 | `{feature-name}-impl.hm.md` | `article-search-impl.hm.md` |
| レビュー記録 | `review-{phase}-{topic}.hm.md` | `review-phase4-auth.hm.md` |
| 手順書 | `phase{N}-{topic}-steps.hm.md` | `phase5-cleanup-steps.hm.md` |
| 解説ガイド | `{topic}-guide.hm.md` | `supabase-auth-guide.hm.md` |

## ドキュメント運用ルール

1. **配置の原則**: 新しいドキュメントは必ず上記のディレクトリ構造に従って配置する。ルートディレクトリ（`doc/` 直下）にファイルを放置しない。
2. **メタデータ**: 各ドキュメントの先頭に `doc/rules/md-rule.md` の front matter を付ける。バージョンは H1 ではなく front matter の `version` で管理する。
3. **ルールの遵守**: `doc/RULE.md` および `doc/rules/` のフォーマットルールに従う。

## Guardrails

- `doc/` 直下にファイルを置かない
- front matter の `version` 更新を忘れない
- 新しいカテゴリが必要な場合は先に `doc/RULE.md` を更新する
