---
name: new-skill
description: このプロジェクトテンプレート用のローカルスキルを新規作成する。
license: Proprietary
compatibility: opencode
metadata:
  domain: project
  audience: project
  output: skill-template
---

## What I do

`project/skills/` 配下に新しいローカルスキルを作成するためのテンプレートと手順を提供します。

## When to use me

- このプロジェクトで新しいローカルスキルが必要になったとき
- プロジェクト固有のルールやワークフローをスキルとして定義したいとき

**スキルを追加すべきものの例:**
- このプロジェクト特有の設計方針や命名規則
- このプロジェクトの開発ワークフロー手順
- このプロジェクト固有のツール設定や運用ルール

**スキルを追加すべきでないものの例:**
- 汎用的なテスト手法やデプロイ手順（グローバルスキルで十分）
- 汎用的なデザイン手法（グローバルスキルで十分）

## Workflow

1. `project/skills/` のどのカテゴリに追加するか決める（`doc/` 等）
2. 新しいディレクトリを作成する: `mkdir -p project/skills/{category}/{skill-name}`
3. 以下のテンプレートに沿って `SKILL.md` を作成する

## SKILL.md テンプレート

```markdown
---
name: {skill-name}
description: {1行で説明}
license: Proprietary
compatibility: opencode
metadata:
  domain: {カテゴリ}
  audience: project
  output: {guidance|direction|review|...}
---

## What I do

{このスキルの役割を簡潔に}

## When to use me

{このスキルを使うべきタイミング}

## Workflow

{具体的な手順}

## Guardrails

{やってはいけないこと、注意点}
```

## スキル設計の指針

- プロジェクト固有の内容だけを書く。汎用的な知識はグローバルスキルに任せる
- 必要になったタイミングで追加すればよく、最初から全てを揃える必要はない
- スキルが増えすぎたら `project/skills/` 内でカテゴリ分けを見直す
