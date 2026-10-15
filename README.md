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
