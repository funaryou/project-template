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
