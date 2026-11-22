# Documentation Rules

## 1. トップレベル構成

```text
doc/
├── materials/     # 全コンテンツ（文書＋画像）
├── rules/         # 文書フォーマットと命名規則
├── RESTORE.md     # CLIが生成する復元手順
├── README.md
└── RULE.md
```

- `materials/` は、本プロジェクトのすべての文書・画像コンテンツを格納します。
- MarkdownはエディタのプレビューまたはGitホスティング上で確認します。
- `RESTORE.md` は `ptcli restore-doc` で更新します。手作業の補足は別の文書に記載します。

## 2. Scope and Purpose
- `materials/architecture/` は、構造・責務分割・データ設計・技術方針を扱う。
- `materials/design/` は、UI/UX・画面設計・体験設計を扱う（`.pen` を含む）。

## 3. Directory Responsibilities
- `materials/architecture/system/`: システム全体構成、責務境界、外部連携方針、技術選定、機能一覧。
- `materials/architecture/database/`: ER 図、テーブル設計、インデックス方針、マイグレーション設計。
- `materials/architecture/structure/frontend/`: フロントエンド構造設計（レイヤ、状態管理、依存関係）。
- `materials/architecture/structure/backend/`: バックエンド構造設計（レイヤ、ユースケース、依存関係）。
- `materials/design/`: 画面設計資料、画面要件定義、プロトタイプ、デザインファイル（例: `design.pen`）。
- `materials/guide/`: 環境構築手順、セットアップガイド、クイックスタート。
- `materials/implementation/`: 実装ガイド、詳細手順、運用ノウハウ。
- `materials/verification/test-plan/`: テスト観点、テスト計画、受け入れ条件。
- `materials/verification/test-result/`: テスト結果、実行ログ要約、既知課題。
- `materials/review/frontend/`, `materials/review/backend/`: レビュー記録。
- `materials/misc/`: 上記に当てはまらない補助資料。
- `materials/temp/`: 一時資料。正式採用時は適切なディレクトリへ移動する。
- `materials/demo/`: デモ用資料、シナリオ、説明補助。
- `materials/image/`: スクリーンショット・図版・画面キャプチャ。
- `materials/prompt/`: プロンプト関連の設計資料・テンプレート・知見。
- `rules/`: 特定カテゴリの文書を書くためのフォーマット定義ルールファイル。
  - 各ルールファイル（`*-rule.md`）は、対象文書の構成・必須セクション・コードの扱いなどを定義する。
  - ルールのフォーマット自体は `rules/RULE.md` に従う。

## 4. Review Document Mandatory Rule
- `materials/review/frontend/` および `materials/review/backend/` に作成するレビュー用 Markdown (`.md`) は、**必ずファイル最下部に担当モデルを明記**する。
- 記載形式は以下で統一する。

```md
担当:<モデル名>
```

- 記載例:

```md
担当:<gpt-5.3-codex>
```

- この記載がないレビュー文書は未完了扱いとする。

## 5. Front matter（必須）
- `materials/` 配下に作成する Markdown は、先頭に YAML 形式の front matter を必ず置く。
- 必須フィールドは `title` / `description` / `author` / `date` / `version` / `status`。任意で `tags` を付ける。
- `version` は引用符で囲み、`date` は `YYYY-MM-DD`、`status` は `draft` / `review` / `approved` / `archived` のいずれかとする。
- `README.md` / `RULE.md` / `AGENTS.md` などの規約・入口ファイルには front matter を付けない。
- 詳細は [`rules/md-rule.md`](./rules/md-rule.md) を正とする。

## 6. ファイル命名
- ファイル名は内容が判別できる具体名を使う。
- 用途でサフィックスを分ける。AI が作成し人間が確認する文書は `<name>.hm.md`、AI 専用は `<name>.ai.md`、人間が作成・維持する文書は `<name>.md`。
- ベース名は小文字 ASCII のケバブケースとし、スペース・大文字・日本語・アンダースコアを使わない。
- `README` / `RULE` / `AGENTS` / `INDEX` / `SKILL` / `RESTORE` は大文字表記で固定し、新たに増やさない。
- 既存構成に新しいカテゴリが必要な場合は、先に `RULE.md` を更新してからディレクトリを追加する。
- 役割が重複する資料は作らず、必要に応じてリンク参照で集約する。
- 詳細は [`rules/md-rule.md`](./rules/md-rule.md) を正とする。

## 7. .gitignore 適用範囲の保護
- `.gitignore` に記載されているファイル・ディレクトリは、AI による編集・作成・変更の対象外とする。
- やむを得ず `.gitignore` 対象のファイルに変更が必要な場合は、先に当該ファイルを `.gitignore` から除外するか、ユーザーの明示的な許可を得ること。
- このルールはプロジェクトルートおよび全サブディレクトリの `.gitignore` に適用される。

## 8. AI 記録領域

### 8-a. AI 自由記録領域: materials/memo/
- `materials/memo/` は、AI が重要・有用と判断した情報を自由に記録してよい領域とする。
- 以下のような情報を積極的に記録してよい：
  - プロジェクトのコンテキストや判断の背景
  - 繰り返し参照される設定値や設計意図
  - 作業中に得た知見や注意点
  - 後から自分（AI）が参照すると生産性が向上する情報
- 記録形式は任意。ファイル分割、箇条書き、Markdown 見出し構成など、AI の判断に委ねる。
- この領域のファイルは AI が自由に新規作成・追記・編集してよい。ユーザーからの明示的な指示は不要とする。

### 8-b. AI 会話ログ領域: materials/memo/ai-logs/
- `materials/memo/ai-logs/` は、ユーザーとの会話内容を定期的に保存するための領域とする。
- 以下の目的で使用する：
  - 長期間の会話コンテキストの保全
  - 過去の設計判断や決定事項の追跡
  - セッションを跨いだ一貫性の維持
- 保存形式は Markdown ファイルとし、ファイル名に日時を含めることを推奨（例: `2026-07-22_session.md`）。
- この領域のファイルは AI が定期的に作成・追記してよい。ユーザーの明示的な指示がなくても、重要な会話内容はここに記録すること。
- `memo.md`（一般メモ）とは異なり、会話の生ログに近い形で保存してよい。
