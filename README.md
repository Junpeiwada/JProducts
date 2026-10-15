# JProducts

Junpei Wada が個人で設計・製作しているハードウェアの紹介サイト。GitHub Pages で公開している。

- 一覧: https://junpeiwada.github.io/JProducts/
- JP-Knob16: https://junpeiwada.github.io/JProducts/jpknob16/

## 構成

```
JProducts/
├── index.html        製品の一覧
└── <製品名>/
    ├── index.html    製品ページ（HTML・CSS・JS を 1 ファイルにまとめる。ビルドなし）
    └── images/
```

製品を足すときは、フォルダを 1 つ作り、`index.html` の一覧にカードを 1 枚足す。

## 画像

- 写真は sRGB に変換し、幅 1200px と 2400px の JPEG にする（`sips -m "/System/Library/ColorSync/Profiles/sRGB Profile.icc" -Z 1200 -s format jpeg -s formatOptions 80`）
- 公開前にメタデータを消す（`exiftool -overwrite_original -all= <ファイル>`）

## ロゴ（`assets/`）

- `jp-mark.svg`: JP マーク。元データは `~/Dropbox/AI/04_ステッカー/JPマーク.ai`（ステッカーの台紙）。`pdftocairo -svg` で SVG にし、左上の 1 個のパスを原点に寄せて取り出した
- `favicon.svg` / `favicon.png`（64px）/ `apple-touch-icon.png`（180px）: 白地にマークを置いたアイコン
- `og.jpg`: 一覧の SNS 用画像（1200×630）。マークの下に「Products」を置いた組み合わせ
