# プロジェクトテンプレート

新しいプロジェクトを始めるためのテンプレートです。以下の手順をターミナルにコピペすると、対話形式でプロジェクトが作成されます。

## セットアップ手順

以下のブロックをターミナルに貼り付けて実行してください。いくつか質問に答えると自動でプロジェクトが作成されます。

> **注意**: 事前に `git` がインストールされていることを確認してください。

```bash
#!/bin/bash
set -e

echo "================================================"
echo "  プロジェクトテンプレート セットアップ"
echo "================================================"
echo ""

# ------------------------------------------------
# 1. プロジェクト名
# ------------------------------------------------
echo "質問 1/3:"
echo -n "プロジェクトディレクトリの名前を入力してください: "
read PROJECT_NAME
while [ -z "$PROJECT_NAME" ]; do
  echo -n "（空です）名前を入力してください: "
  read PROJECT_NAME
done

# ------------------------------------------------
# 2. AI エージェントの選択
# ------------------------------------------------
echo ""
echo "質問 2/3:"
echo "使用する AI エージェントを選択してください（番号入力）:"
echo "  1) opencode"
echo "  2) claude-code"
echo "  3) codex"
echo "  4) cursor"
echo "  5) continue"
echo "  6) windsurf"
echo "  7) その他（自分で指定）"
echo "  8) なし（何もしない）"
echo -n "番号を入力 [1-8]: "
read AGENT_NUM

case "$AGENT_NUM" in
  1) AGENT_NAME="opencode";        AGENT_DIR=".opencode" ;;
  2) AGENT_NAME="claude-code";     AGENT_DIR=".claude" ;;
  3) AGENT_NAME="codex";           AGENT_DIR=".codex" ;;
  4) AGENT_NAME="cursor";          AGENT_DIR=".cursor" ;;
  5) AGENT_NAME="continue";        AGENT_DIR=".continue" ;;
  6) AGENT_NAME="windsurf";        AGENT_DIR=".windsurf" ;;
  7)
    echo -n "使用するディレクトリ名を入力（例: .myagent/skills）: "
    read AGENT_DIR
    AGENT_NAME="custom"
    ;;
  8) AGENT_NAME="none"; AGENT_DIR="" ;;
  *) echo "無効な番号です。スキップします。"; AGENT_NAME="none"; AGENT_DIR="" ;;
esac

# ------------------------------------------------
# 3. ドキュメントプレビューポート
# ------------------------------------------------
echo ""
echo "質問 3/3:"
echo -n "ドキュメントプレビューのポート番号を入力（none でスキップ、推奨: 8080-65535）: "
read DOC_PORT

if [ "$DOC_PORT" != "none" ] && [ -n "$DOC_PORT" ]; then
  if ! [[ "$DOC_PORT" =~ ^[0-9]+$ ]] || [ "$DOC_PORT" -lt 1024 ] || [ "$DOC_PORT" -gt 65535 ]; then
    echo "→ 無効なポート番号です。デフォルト（8080）を使用します。"
    DOC_PORT=""
  fi
else
  DOC_PORT=""
fi

# ------------------------------------------------
# クローン作成
# ------------------------------------------------
echo ""
echo "================================================"
echo "  プロジェクトを作成しています..."
echo "================================================"
echo ""

REPO_URL="https://github.com/funaryou/project-template.git"

git clone "$REPO_URL" "$PROJECT_NAME"
cd "$PROJECT_NAME"

# ------------------------------------------------
# 演習用ディレクトリ
# ------------------------------------------------
echo "→ 演習用ディレクトリを作成しています..."
mkdir -p demo
echo "  ✓ demo/ を作成しました（demo-exercise スキルの演習領域）"

# ------------------------------------------------
# AI エージェント設定
# ------------------------------------------------
if [ "$AGENT_NAME" != "none" ] && [ -d "skills" ]; then
  echo "→ $AGENT_NAME 用の設定ディレクトリを作成しています..."
  mkdir -p "$AGENT_DIR/skills"
  cp -r skills/* "$AGENT_DIR/skills/"
  rm -rf skills
  echo "  ✓ skills/ → $AGENT_DIR/skills/ にコピーしました"
fi

# ------------------------------------------------
# ドキュメントプレビューポート設定
# ------------------------------------------------
if [ -n "$DOC_PORT" ] && [ -f "doc/serve.js" ]; then
  echo "→ ポートを $DOC_PORT に設定しています..."
  if [[ "$OSTYPE" == "darwin"* ]]; then
    sed -i '' "s/PORT = parseInt(process.argv\[2\], 10) || [0-9]*;/PORT = parseInt(process.argv[2], 10) || $DOC_PORT;/" doc/serve.js
  else
    sed -i "s/PORT = parseInt(process.argv\[2\], 10) || [0-9]*;/PORT = parseInt(process.argv[2], 10) || $DOC_PORT;/" doc/serve.js
  fi
  echo "  ✓ doc/serve.js のポートを $DOC_PORT に変更しました"
fi

# ------------------------------------------------
# クリーンアップ
# ------------------------------------------------
echo "→ セットアップファイルを削除しています..."
rm -f README.md package.json package-lock.json 2>/dev/null || true
rm -rf .git 2>/dev/null || true
echo "  ✓ README.md と .git を削除しました"

echo ""
echo "================================================"
echo "  完了！プロジェクト $PROJECT_NAME を作成しました"
echo "================================================"
echo ""
echo "次のコマンドでプロジェクトに移動してください:"
echo "  cd $PROJECT_NAME"
echo ""
echo "ドキュメントプレビュー:"
echo "  bash doc/serve.sh"
```

## 生成後のフォルダ構成

セットアップ完了後のプロジェクトは以下の構成になります。

```text
<PROJECT_NAME>/
├── demo/                 # 演習用ディレクトリ（セットアップ時に自動作成）
├── doc/                  # ドキュメント管理・プレビュー用
├── project/              # 実装用ディレクトリ（初期状態は空）
└── .opencode/skills/     # AIエージェント用スキル（選択したエージェント名で変化）
```

> **注意**: セットアップ時に `README.md`、`package.json`、`package-lock.json`、`.git` は削除されます。
> この `README.md` はテンプレート用の手順書であり、生成後のプロジェクトには残りません。

### 各フォルダの役割

| フォルダ | 役割 | 補足 |
|---------|------|------|
| `demo/` | 演習用領域。`demo-exercise` スキルの演習で使用します。セットアップ時に空で作成されます | 成果物置き場ではなく、試行・練習用です |
| `doc/` | 文書コンテンツとプレビューサーバーを格納します。`bash doc/serve.sh` でブラウザプレビューできます | 詳細なルールは `doc/RULE.md` を参照してください |
| `doc/materials/` | すべての文書・画像コンテンツの格納場所です。`architecture/`、`design/`、`guide/`、`implementation/`、`verification/`、`review/`、`memo/` 等に分類して保存します | 新しいカテゴリ追加時は先に `doc/RULE.md` を更新します |
| `doc/src/` | `materials/` をブラウザでプレビューするためのフロントエンドアプリ（`index.html`、`style.css`、`script.js`）です | 直接編集は原則不要です |
| `doc/rules/` | 特定カテゴリの文書フォーマット定義（`*-rule.md`）を格納します | ルールの書き方自体は `doc/rules/RULE.md` に従います |
| `doc/serve.js` / `doc/serve.sh` | プレビュー用開発サーバー本体と起動スクリプトです。`materials/` の変更を検出して SSE でブラウザに通知します | ポート番号はセットアップ時の質問3で自動設定されます |
| `project/` | 成果物・実装コードの置き場です。初期状態は `.gitkeep` のみの空ディレクトリです | ここにアプリケーション本体を作成します |
| `.opencode/skills/` （可変） | AIエージェント用ローカルスキル置き場です。セットアップ時の質問2で選択したエージェント名に応じたディレクトリ（例: `.opencode`、`.claude`、`.cursor` 等）の配下に `skills/` の内容がコピーされます | 元の `skills/` ディレクトリはコピー後に削除されます。「なし」を選択した場合は `skills/` のまま残ります |
| `skills/doc/` | ドキュメント作成支援スキル（`architecture/`、`workflow/`、`rules/`、`ai-logging/`）です | 生成後は `<AGENT_DIR>/skills/doc/` に移動します |
| `skills/project/_template/` | 新規スキル作成用のテンプレート置き場です | 新しいローカルスキルが必要になったら `new-skill` スキルの手順に従います |
| `skills/demo/demo-exercise/` | `demo/` を使った演習用スキルです | 使い方の習得・試行用です |
| `skills/new-skill/SKILL.md` | このプロジェクト専用の新規ローカルスキル作成手順です | 生成後は `<AGENT_DIR>/skills/new-skill/` に移動します |
