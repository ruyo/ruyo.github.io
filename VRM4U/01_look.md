---
title: "見た目を調整する"

gallery:
  - url: /VRM4U/assets/images/010_top.png
    image_path: /VRM4U/assets/images/010_top.png

gallery2:
  - url: /VRM4U/assets/images/010_release.png
    image_path: /VRM4U/assets/images/010_release.png

# {% include gallery id="gallery" caption="This is a sample gallery with **Markdown support**." %}

# {% include gallery id="gallery2" %}

# [![](./assets/images/010_release.png)](../assets/images/010_release.png)

# [![](/assets/images/010_release.png)](/assets/images/010_release.png)

# [![](/VRM4U/assets/images/010_release.png)](https://ruyo.github.io/VRM4U/assets/images/010_release.png)

---


||
|-|
|[![](./assets/images/01b_top.png)](../assets/images/01b_top.png)|

----

## 輪郭線とシャドウを有効化する

以下のメニューのチェックボックスをONにして、VRM4Uフォルダを表示します。

||
|-|
|[![](./assets/images/01a_plugin.png)](../assets/images/01a_plugin.png)|


`VRM4U Content/Util/Actor` から、`MToonAttachActor` を配置します。ドラッグ＆ドロップです。

||
|-|
|[![](./assets/images/01a_mtoon1.png)](../assets/images/01a_mtoon1.png)|


下図の番号順にクリックしてください。
スポイトアイコンをクリックし、その後キャラクタをクリックします。

||
|-|
|[![](./assets/images/01a_click.png)](../assets/images/01a_click.png)|


輪郭線とセルフシャドウが有効化されました。

||
|-|
|[![](./assets/images/01a_end.png)](../assets/images/01a_end.png)|


----

## 色味を調整する

`VRM4U Content/Util/Actor` から、`MToonMaterialSystem` を配置します。

||
|-|
|[![](./assets/images/01a_sys1.png)](../assets/images/01a_sys1.png)|


`details` よりパラメータを適当に変更してみましょう。
特殊描画（輪郭線の太さ、MatCap強度、色のガンマ補正）から、ライト（オフセット、Exposure基準）を変更できます。

一部のパラメータは、Litモード（後述します）のみ反応します。

|||
|-|-|
|[![](./assets/images/01a_syspanel.png)](../assets/images/01a_syspanel.png)|.................................................|

ここでは大まかにキャラクタ全体の見た目を調整することができます。
同じ調整はマテリアル個別でも可能です。応用編で解説します。

||
|-|
|[![](./assets/images/01a_sys2.png)](../assets/images/01a_sys2.png)|


----

## ライティングする


`AssetUtil`を配置します。

||
|-|
|[![](./assets/images/01b_asset.png)](../assets/images/01b_asset.png)|


下図の順にクリックします。LitチェックボックスをONにします。

||
|-|
|[![](./assets/images/01b_asset2.png)](../assets/images/01b_asset2.png)|


ライトが反映されるようになります。

||
|-|
|[![](./assets/images/01b_light2.png)](../assets/images/01b_light2.png)|

上記手順は、インポート時にも設定可能です。Litマテリアルでインポートしてください。

||
|-|
|[![](./assets/images/01b_import.png)](../assets/images/01b_import.png)|

----
## 見た目の調整 その先へ

上手くライティングすると素敵な見た目になります。
詳しくは応用編へどうぞ。


