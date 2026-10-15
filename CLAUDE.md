# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 概要

Junpei Wada が個人で設計・製作しているハードウェアの紹介サイト。GitHub Pages（`https://junpeiwada.github.io/JProducts/`）で公開する静的サイトで、**ビルド・パッケージ管理・テスト・lint は無い**。HTML ファイルを直接編集し、ブラウザで開いて確認する。

## 構成

- `index.html` — 製品の一覧。製品ごとに `<a class="product">` のカードを 1 枚置く
- `<製品名>/index.html` — 製品ページ。HTML・CSS・JS を 1 ファイルにまとめる（外部 CSS/JS ファイルは作らない）
- `<製品名>/images/` — その製品の画像と、製品ページ用の `og.jpg`（1200×630）
- `assets/` — サイト共通のロゴ（`jp-mark.svg`）、favicon、apple-touch-icon、一覧ページ用の `og.jpg`（1200×630）

製品を足すときは、フォルダを 1 つ作り、`index.html` の一覧にカードを 1 枚足す。

## ページ間で揃えている決まりごと

共通 CSS ファイルは無く、各 `index.html` の `<style>` に同じものを書いている。片方を変えたらもう片方も揃える。

- デザイントークンは `:root` の CSS 変数（`--bg` `--ink` `--ink-2` `--line` `--lime` `--lime-ink` `--lime-soft` `--font-display` など）。色は直書きせず変数を使う
- フォントは Google Fonts の Space Grotesk（見出し）・Noto Sans JP（本文）・JetBrains Mono（ラベル類）
- 本文幅は `.wrap`（最大 1120px、左右 24px、760px 以下で 16px）
- ロゴは `assets/jp-mark.svg`（`.lockup` はロゴ＋小さな文字の組）。製品ページからは `../assets/` で参照する
- OGP は `og:url` / `og:image` を `https://junpeiwada.github.io/JProducts/...` の絶対 URL で書く
- 見出しの改行位置は `word-break: auto-phrase` と `.nb`（inline-block）で調整している

## 製品ページ（jpknob16）の JS

末尾の `<script>` は IIFE 1 つで、製品の正面図を SVG で描き、ノブ・キーを操作すると写真編集画面のデモが反応する。

- 正面図の座標は mm 単位（原点はケース左上、試作機の写真から採寸）。`OLED_X` `KNOB_DX` などの定数で配置する
- `PARAMS`（16 個のパラメータ。OLED 4 枚 × 4 で、ノブの並びと同じ順）と `PHOTOS`（3 枚の風景イラストと初期補正値）がデモのデータ
- ノブはホイール・ドラッグ・キーボード、キーはポインタ・Enter/Space で操作できる。アクセシビリティのため両方を維持する

## 画像

- 写真は sRGB に変換し、幅 1200px と 2400px の JPEG にする（`*-1200.jpg` / `*-2400.jpg`）:
  `sips -m "/System/Library/ColorSync/Profiles/sRGB Profile.icc" -Z 1200 -s format jpeg -s formatOptions 80 <ファイル>`
- 公開前にメタデータを消す: `exiftool -overwrite_original -all= <ファイル>`
- `<img>` には `width` / `height`、ファーストビュー以外は `loading="lazy"`、それと写っているものを具体的に書いた日本語の `alt` を付ける
