# fonts

グラフ（matplotlib）のラベルを日本語表示するためのフォントです。

## BIZUDPGothic-Regular-subset.ttf

- 元フォント: **BIZ UDPGothic Regular**（Morisawa / The BIZ UDGothic Project Authors）
- 入手元: https://github.com/google/fonts/tree/main/ofl/bizudpgothic
- ライセンス: **SIL Open Font License 1.1**（`OFL.txt` を参照）
  - 予約フォント名（Reserved Font Name）の指定はないため、サブセット後もフォント名は `BIZ UDPGothic` のままです。
- 変更点（サブセット処理）:
  - 収録文字を **ASCII + かな + 全角記号 + Shift-JIS(cp932)相当の漢字 + 理科系記号** に限定
  - ヒンティングを除去（matplotlibは既定で `text.hinting: force_autohint` のため描画に影響しません）
  - 4.5MB → **約2.0MB**
- 再生成コマンド（参考）:
  ```
  pyftsubset BIZUDPGothic-Regular.ttf --text-file=cs.txt \
    --output-file=BIZUDPGothic-Regular-subset.ttf --no-hinting --drop-tables+=DSIG
  ```

## 使われ方

`index.html` の初期化時に fetch → Pyodideの仮想FS（`fonts/jp.ttf`）へ書き込み →
`font_manager.addfont()` で登録し `rcParams["font.family"] = "BIZ UDPGothic"` を設定します。
読み込みに失敗した場合もグラフ自体は動作します（日本語が□になるだけ）。
