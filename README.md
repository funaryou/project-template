## project-template

`ptcli` が配布する文書・AI用スキルの原本です。テンプレートの変更は、このリポジトリの `doc/` と `skills/` に反映します。

| ディレクトリ | 用途 |
|--------------|------|
| `doc/` | 配布する文書テンプレート |
| `skills/` | 配布するAI用スキル |
| `project/` | 既存の空ディレクトリ。npmへの配布対象外です |

## ptcliとの関係

[ptcli](https://github.com/funaryou/ptcli) は、このリポジトリの特定コミットを `assets/template/` のGit submodule（別リポジトリのコミットを固定して参照する仕組み）として使用します。

npm公開時には `doc/` と `skills/` の実ファイルを同梱するため、CLI利用者によるGitやsubmoduleの操作は不要です。

## テンプレートの更新

1. このリポジトリの `doc/` または `skills/` を編集し、変更をコミットして `master` へpushします。
2. `ptcli` リポジトリで参照コミットを更新します。

```bash
# ptcliのルートで実行します
git submodule update --init --remote -- assets/template
git diff --submodule=log
npm test
git add assets/template
git commit -m "chore: update bundled template"
```

3. `ptcli` のバージョンを更新し、mainとバージョンタグをpushしてnpmへ公開します。

テンプレートのpushだけでは、`ptcli` の参照コミットと公開済みnpmパッケージは更新されません。submoduleの固定参照により、過去のCLIが使用したテンプレートを再現できます。

CLIの利用・公開手順は [ptcli README](https://github.com/funaryou/ptcli/blob/main/README.md) を参照してください。
