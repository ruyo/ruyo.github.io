---
title: "VRChat用アバターをVRMにして読む"
---

||
|-|
|[![](./assets/images/small/04a_top.png)](../assets/images/04a_top.png)|
|モデル：[NecoMaid](https://booth.pm/ja/items/1843586) （fbx -> VRM変換）|
|アニメーション：[ミライ小町](https://www.bandainamcostudios.com/works/miraikomachi/dlcguideline.html)（fbx -> humanoidリターゲット）|

----

## UnityでVRM変換する

### 手軽な方法、Unityわからない人向け
Unityにインポートし、そのままVRM出力するだけでOK。
Unity上でのプレビューが紫色でも問題ない。ただし揺れ骨は動かない。

### Unity詳しい人向け

ある程度MToonマテリアルを組んでおくと後段の手順が減る。
DynamicBoneからVRMSpringBoneへの置き換え、BlendShapeの登録をしておくとさらにスムーズ。

----
## マテリアルをセットアップする

前段でそのまま出力した人向け。
インポート時のマテリアル最適化をOFFする。
テクスチャを2箇所セットすればOK。

影色はMToonMaterialSystemで一括適用できる。マテリアル毎に設定しても良い。

他の調整は基礎編や撮影編へ。

----
## 目を前面に描画する（中級者向け）

StencilMaskを利用する。目や眉毛が前髪より手前に描画される。

マテリアル設定により、Stencilが2の場所について、透明度を任意に設定できるようになる。

|||
|-|-|
|[![](./assets/images/small/04a_mask1.png)](../assets/images/04a_mask1.png)|[![](./assets/images/small/04a_mask2.png)](../assets/images/04a_mask2.png)|

----

## AngelRingを描画する（上級者向け）

UV2でAngelRingを設定しているモデルのみ。
UniVRM（の中のUniGLTF）を拡張しUV2を利用します。

|AngelRingなし|AngelRingあり|
|-|-|
|[![](./assets/images/small/04a_angel2.png)](../assets/images/04a_angel2.png)|[![](./assets/images/small/04a_angel3.png)](../assets/images/04a_angel3.png)|
|モデル：[幽狐族のお姉様](https://booth.pm/ja/items/1484117) （fbx -> VRM変換）|





### UniGLTFでUV2を出力する

起点のソースは`MeshExporter.cs`です。

キーワード`TEXCOORD_0`で検索し、その行の後ろに`TEXCOORD_1`として同じ処理を追加します。
`TEXCOORD_0`のデータ作成時に`.uv`を参照している箇所があります。`TEXCOORD_1`向けには`.uv2`に書き換えます。

Unityでソースをビルドすると何度かエラーが出ます。その都度 `TEXCOORD_1`の処理を追加すればOKです。

### テクスチャをセットする

マテリアル設定により、テクスチャを設定すればOKです。

||
|-|
|[![](./assets/images/small/04a_angel1.png)](../assets/images/04a_angel1.png)|

厳密には再現されません。簡略化した処理を行っています。
