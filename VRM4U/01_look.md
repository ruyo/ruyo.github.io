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


----
## 輪郭線とシャドウを有効化する

以下のメニューのチェックボックスをONにして、VRM4Uフォルダを表示します。

<figure>
  <img src="./assets/images/01a_plugin.png" width=60%>
</figure>

`VRM4U Content/Util/Actor` から、`MToonAttachActor` を配置します。ドラッグ＆ドロップです。

<img src="./assets/images/01a_mtoon1.png" width=60%>

下図の番号順にクリックしてください。
スポイトアイコンをクリックし、その後キャラクタをクリックします。

<img src="./assets/images/01a_click.png" width=60%>

輪郭線とセルフシャドウが有効化されました。
<img src="./assets/images/01a_end.png" width=60%>

----## 色味を調整する

`VRM4U Content/Util/Actor` から、`MToonMaterialSystem` を配置します。

<img src="./assets/images/01a_sys1.png" width=60%>

`details` よりパラメータを適当に変更してみましょう。
特殊描画（輪郭線の太さ、MatCap強度、色のガンマ補正）から、ライト（オフセット、Exposure基準）を変更できます。

一部のパラメータは、Litモード（後述します）のみ反応します。

<img src="./assets/images/01a_syspanel.png" width=60%>

ここでは大まかにキャラクタ全体の見た目を調整することができます。
同じ調整はマテリアル個別でも可能です。応用編で解説します。

<img src="./assets/images/01a_sys2.png" width=60%>

----
## ライティングする


`AssetUtil`を配置します。

<img src="./assets/images/01b_asset.png" width=60%>

下図の順にクリックします。LitチェックボックスをONにします。

<img src="./assets/images/01b_asset2.png" width=60%>

ライトが反映されるようになります。

<img src="./assets/images/01b_light2.png" width=60%>

上記手順は、インポート時にも設定可能です。Litマテリアルでインポートしてください。

<img src="./assets/images/01b_import.png" width=60%>

----
## 見た目の調整 その先へ

上手くライティングすると素敵な見た目になります。
詳しくは応用編へどうぞ。


