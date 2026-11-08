# Cabernet2d マニュアル

iRIC ソルバー Cabernet2d の日本語マニュアル（Sphinx製）です。

公開版: https://i-ric.org/yasu/cabernet/index.html
（このリポジトリを GitHub Pages で公開するよう設定した後は、そちらの URL に順次切り替え予定）

## 構成

- `source/` — マニュアル本文（reStructuredText）と画像
- `Makefile` / `make.bat` — Sphinx ビルド用

## ローカルでビルドして確認する

```bash
pip install -r requirements.txt
sphinx-build -M html source build
```

`build/html/index.html` をブラウザで開くとプレビューできます（`build/` はコミット対象外）。

## 公開の仕組み

`main` ブランチに push すると、GitHub Actions（`.github/workflows/pages.yml`）が自動的に
Sphinx でビルドし、GitHub Pages に公開します。手動でのアップロード作業は不要です。

## マニュアルを更新する

1. `source/*.rst` を編集（必要なら `source/images_*` に画像を追加）
2. ローカルでビルドして見た目を確認
3. `main` ブランチへ commit・push すれば、数分後に公開版へ反映されます
