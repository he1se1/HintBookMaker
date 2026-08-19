# HintBookMaker

MarkdownファイルからPowerPoint（`.pptx`）スライドを自動生成するツールです。

## 特徴・要件

- インストール不要で `uvx` を使ってGitHubから直接実行可能
- [uv](https://github.com/astral-sh/uv) がインストールされている環境であればすぐに動かせます

---

## 使い方 (uvx で直接実行)

リポジトリをクローンすることなく、`uvx` でGitHubリポジトリを指定して直接実行できます。


### 基本実行
カレントディレクトリにある `slides.md` を使って `output.pptx` を生成します。
※カレントディレクトリに `template.pptx` が存在しない場合は、GitHubから自動的にデフォルトテンプレートがダウンロードされます。

```bash
uvx --from git+https://github.com/he1se1/HintBookMaker hintbookmaker
```

### オプション指定
ファイル名やパスを明示的に指定する場合：

```bash
# Markdownファイルを指定
uvx --from git+https://github.com/he1se1/HintBookMaker hintbookmaker -i slides.sample.md

# テンプレートや出力先を指定
uvx --from git+https://github.com/he1se1/HintBookMaker hintbookmaker -i input.md -t custom_template.pptx -o result.pptx

# ヘルプ確認
uvx --from git+https://github.com/he1se1/HintBookMaker hintbookmaker --help
```

### コマンドライン引数・オプション一覧

| オプション | デフォルト値 | 説明 |
| :--- | :--- | :--- |
| `-i`, `--input` | `slides.md` | 入力となるMarkdownファイルのパス |
| `-t`, `--template` | `template.pptx` | ベースとなるPowerPointテンプレートファイルのパス（未配置時はGitHubから自動取得） |
| `-o`, `--output` | `output.pptx` | 生成されるPowerPointファイルの出力先パス |
| `--layout` | `1` | テンプレート内で使用するスライドレイアウトのインデックス番号 |
| `-h`, `--help` | - | ヘルプメッセージを表示して終了 |


---

## ローカル開発 / リポジトリをクローンして使う場合

```bash
# クローン
git clone https://github.com/he1se1/HintBookMaker.git
cd HintBookMaker

# 依存関係の同期
uv sync

# 実行
uv run hintbookmaker -i slides.sample.md
```

---

## Markdownのフォーマット仕様

スライドごとに `---` で区切ります。

```markdown
# スライド1 タイトル
## 1
ヒント1の内容がここに入ります。
## 2
ヒント2の内容や答えがここに入ります。
---
# スライド2 タイトル
## 1
2は省略可能です。
---
# スライド3 タイトル
## 1
丸ごと省略することもできます。
```

- `# スライドタイトル`: スライドのタイトル（プレースホルダー0番）
- `## 1`: 本文1（プレースホルダー1番）
- `## 2`: 本文2（プレースホルダー2番）
- `---`: スライドの区切り

※ テンプレート側の構造（プレースホルダーやレイアウト構成）に合わせて適宜 `--layout` オプション等をご利用ください。
