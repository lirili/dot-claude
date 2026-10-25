# dot-claude

Claude Code のルール、開発フローの元文書、skill、サブエージェント定義。`~/.claude` に取り込んで使う。

## 構成

- `CLAUDE.md`: すべての作業に共通するルール。Claude Code が読む。
- `docs/`: 開発フローの元文書。`dev-flow.md` が工程の骨格、`dev-flow-<分野>.md` が分野に固有の内容（開発分野は `dev-flow-code.md`）で、skill は元文書から反映する。
- `skills/`: 個人用の skill。`skills/synced/` は claude.ai から同期される skill の置き場で、追跡しない。
- `agents/`: サブエージェント定義。
- `.gitignore`: 許可一覧方式。Claude Code の実行時ファイルや個人設定は追跡しない。

## セットアップ

`~/.claude` は Claude Code が実行時ファイルを置くディレクトリなので、clone ではなく init と fetch で取り込む。ディレクトリがなければ先に作る。追跡対象と同名のファイルが既にある場合は、退避してから実行する。

```powershell
Set-Location $HOME\.claude
git init -b main
git remote add origin https://github.com/lirili/dot-claude.git
git fetch origin
git checkout -B main origin/main
```

新しい Claude Code セッションで、ファイルを読まずに `CLAUDE.md` の内容を引用できれば取り込みは有効。`agents/` の定義は、セッション開始時に `~/.claude/agents` が無かった場合、Claude Code の再起動後に読まれる。

## 更新

開発フローのルールの変更は `docs/` の元文書を先に更新し、承認を得てから skill に反映する（`docs/dev-flow.md` の「skillへの反映」）。

## 前提にしている値

各セッションのモデルとエフォートは開始時に選び、サブエージェントのモデルとエフォートは `agents/` の定義で決める。セッションごとの既定値は `docs/dev-flow.md` の役割「セッション」に定める。既定値は目安で、実際のモデルとエフォートは都度ユーザーが選ぶ。

## ライセンス

MIT License（`LICENSE`）。ライセンスの本文は原文の英語のまま置き、翻訳は付けない。
