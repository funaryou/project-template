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

| 種類 | 命名パターン | 例 |
| :--- | :--- | :--- |
| 実装記録 | `impl_{feature_name}.md` | `impl_article_search.md` |
| レビュー記録 | `review_{phase}_{topic}.md` | `review_phase4_auth.md` |
| 手順書 | `phase{N}_{topic}_steps.md` | `phase5_cleanup_steps.md` |
| 解説ガイド | `{topic}_guide.md` | `supabase_auth_guide.md` |

## ドキュメント運用ルール

1. **配置の原則**: 新しいドキュメントは必ず上記のディレクトリ構造に従って配置する。ルートディレクトリ（`doc/` 直下）にファイルを放置しない。
2. **バージョン管理**: 各ドキュメントの H1 見出しの末尾に `[#N]` 形式でバージョンを記載する。内容を更新したらインクリメントする。
3. **ルールの遵守**: `doc/RULE.md` および `doc/rules/` のフォーマットルールに従う。

## Guardrails

- `doc/` 直下にファイルを置かない
- バージョン番号のインクリメントを忘れない
- 新しいカテゴリが必要な場合は先に `doc/RULE.md` を更新する
