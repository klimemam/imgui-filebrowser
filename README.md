# imgui-filebrowser

viewer の File Browse パネルを、他のホストからもリンクできる形に切り出したもの。
**現状: 準備段階。** ソースはまだ viewer 側 (`core/browse/`) にあり、切り出しの設計と
進行状況は viewer の `docs/browse-extract-design.md` が正典。

## 形(設計で決まっていること)

- **ソース配布**。ビルド済みバイナリは配らない
- **ホストが提供するもの**: 形式表 (`imagefile.h` 相当) と Dear ImGui
- **継ぎ目はリンク時契約1本**。関数ポインタ表は使わない —— 位置初期化の表は
  同型スロットの取り違えをリンカが検査できないため
- **「準備完了」の定義**: viewer 側の `linktest`(browse を別リンク単位でビルドする
  CI ターゲット)が緑であること。実際に別リンク単位でビルドが通ることが、
  切り出せることの唯一の証明

## 経緯

- 切り出しの実体は viewer 内の第3層(`extern App app` の直接読み書き、32 フィールド
  約 120 箇所)の解体。棚卸しと設計: viewer `docs/browse-inventory.md` /
  `docs/browse-extract-design.md`
- この repo は 2026-08-14 のユーザー裁定で先行作成された(裁定: 「新規レポジトリを
  作れるならそれで」)。中身の移植は linktest 緑の後

## ライセンス

Apache License 2.0([LICENSE](LICENSE))。viewer 本体と同じ(2026-08-17 裁定)。
