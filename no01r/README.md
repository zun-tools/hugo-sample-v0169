# hugo/no01r サンプル（動画「Hugo入門」の最終形）

動画の最後にできあがるブログ一式です。公式の Quick Start で作ったプロジェクトに、次を加えた状態です。

- テーマ Ananke を git submodule で `v2.19.1` に固定（`themes/ananke`）
- `.gitignore` に `.hugo_build.lock` と `public/`
- 自分の側で直したフッター 1 枚
- 記事 2 本（1 本目は公開、2 本目は下書き）

## 動かし方

```bash
git clone --recurse-submodules https://github.com/zun-tools/hugo-sample.git
cd hugo-sample/no01r
hugo server -D
```

`-D` を付けると下書きの記事も見えます。付けないと、公開する記事（1 本目）だけです。
公開用のファイルを作るだけなら `hugo` を実行します（`public/` ができます。git には入れません）。

## 自分の側で直した 1 枚

`layouts/_partials/site-footer.html`

テーマの同名ファイルをコピーして、2 か所だけ直しました。背景色（`bg-black` を `bg-dark-green` へ）と、年表示のあとの一言です。
年表示は残してあります。Hugo は自分のプロジェクトの `layouts/` を先に読むので、テーマ本体（`themes/ananke`）は触らずに済みます。

## テーマの版を上げる手順

```bash
git submodule update --remote --merge
git -C themes/ananke diff <前の版> HEAD --stat   # 差分を見る
git add themes/ananke
git commit -m "Ananke を <新しい版> へ更新"       # 記録
```

## 確かめたこと

- Hugo v0.169.0（extended）と Ananke v2.19.1 の組み合わせで、`hugo` が警告・エラーなしで通ること
- 確かめた環境は Linux（arm64）です

## ライセンス

自作部分（設定・記事・フッターの直し）は MIT です。Ananke は MIT で、作者のものです。
