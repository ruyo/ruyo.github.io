---
title: "見た目を調整する"

#gallery:
#  - url: /VRM4U/assets/images/010_top.png
#    image_path: /VRM4U/assets/images/010_top.png

#gallery2:
#  - url: /VRM4U/assets/images/010_release.png
#    image_path: /VRM4U/assets/images/010_release.png

# {% include gallery id="gallery" caption="This is a sample gallery with **Markdown support**." %}

# {% include gallery id="gallery2" %}

# [![](./assets/images/small/010_release.png)](../assets/images/010_release.png)

# [![](/assets/images/010_release.png)](/assets/images/010_release.png)

# [![](/VRM4U/assets/images/010_release.png)](https://ruyo.github.io/VRM4U/assets/images/010_release.png)

---


||
|-|
|[![](./assets/images/small/01b_top.png)](../assets/images/01b_top.png)|
|モデル：[ヴィータ](https://hub.vroid.com/characters/6193066630030526355/models/3525604181073039892)|

----

## 輪郭線とシャドウを有効化する

以下のメニューのチェックボックスをONにして、VRM4Uフォルダを表示します。

||
|-|
|[![](./assets/images/small/01a_plugin.png)](../assets/images/01a_plugin.png)|


`VRM4U Content/Util/Actor` から、`MToonAttachActor` を配置します。ドラッグ＆ドロップです。

||
|-|
|[![](./assets/images/small/01a_mtoon1.png)](../assets/images/01a_mtoon1.png)|


下図の番号順にクリックしてください。
スポイトアイコンをクリックし、その後キャラクタをクリックします。

||
|-|
|[![](./assets/images/small/01a_click.png)](../assets/images/01a_click.png)|


輪郭線とセルフシャドウが有効化されました。

||
|-|
|[![](./assets/images/small/01a_end.png)](../assets/images/01a_end.png)|


----

## 色味を調整する

`VRM4U Content/Util/Actor` から、`MToonMaterialSystem` を配置します。

||
|-|
|[![](./assets/images/small/01a_sys1.png)](../assets/images/01a_sys1.png)|


`details` よりパラメータを適当に変更してみましょう。
特殊描画（輪郭線の太さ、MatCap強度、色のガンマ補正）から、ライト（オフセット、Exposure基準）を変更できます。

一部のパラメータは、`Lit`モード（後述します）のみ反応します。

|||
|-|-|
|[![](./assets/images/small/01a_syspanel.png)](../assets/images/01a_syspanel.png)|.................................................|

大まかにキャラクタ全体の見た目を調整することができます。
シーンに応じて、明暗や色味、リアル寄り/アニメ寄り を調整することができます。

同じ調整はマテリアル個別でも可能です。応用編で解説します。

||
|-|
|[![](./assets/images/small/01a_sys2.png)](../assets/images/01a_sys2.png)|


----

## ライティングする

初期状態のマテリアルはライトが反映されません。`Unlit`モードになっています。
これを`Lit`モードに切り替えます。

`AssetUtil`を配置します。

||
|-|
|[![](./assets/images/small/01b_asset.png)](../assets/images/01b_asset.png)|


下図の順にクリックします。LitチェックボックスをONにして、スポイトをクリック、キャラを選択します。その後 `ChangeParentMat` ボタンを押します。

||
|-|
|[![](./assets/images/small/01b_asset2.png)](../assets/images/01b_asset2.png)|


マテリアルが切り替わり、ライトが反映されるようになります。

||
|-|
|[![](./assets/images/small/01b_light2.png)](../assets/images/01b_light2.png)|

上記手順は、インポート時にも設定可能です。Litマテリアルでインポートしてください。

||
|-|
|[![](./assets/images/small/01b_import.png)](../assets/images/01b_import.png)|

----
## 見た目の調整 その先へ

上手くライティングできるようになると、モデルを様々なシーンに配置できるようになります。詳しくは応用編を参照ください。

なお応用編の調整内容は`Lit`モードによるものです。

[次の章へ](../01_animation/)
