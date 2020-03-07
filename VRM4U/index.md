---
title: "VRM4U"

share: true

#gallery:
#  - url: /VRM4U/assets/images/010_top.png
#    image_path: /VRM4U/assets/images/010_top.png
---

## はじめに
**VRM4U**はUE4で動作する、VRMファイルのインポーターです。

[導入はこのリンクから](./01_quick-start/)

## 特徴

|||
|----|----|
|![](/assets/images/03.png)|![](/assets/images/04.png)|
|![](/assets/images/01.png)|![](/assets/images/02.png)|


 - VRMファイルをインポートできます。
 - アニメーション
     - 手軽にリターゲット可能です。A-pose/T-pose、RIGが生成されます。
     - 揺れ骨にVRMSpringBoneを利用可能です。PhysicsAssetも選択できます。
     - 顔アニメ（Morphtarget・BlendShapeGroup）も利用可能です。
 - マテリアル
     - MToonを再現したマテリアル。影色の指定や、アウトラインの色・太さ調整、MatCapなどが全て適用されます。
     - 既存のPBR背景の中にキャラクタを描画できます。既存のポストプロセスにも馴染みます。
     - レイトレースを利用可能です。PBRに合わせるための拡張機能もあります。
 - モバイル 利用可能
     - BoneMapリダクション機能により手軽に表示可能です。
     - 描画クオリティを選択できます。ロースペック対応です。
 - VR/AR 利用可能
     - シンプルな機能で構成しているため破綻しません。
     - 描画はForward/Deferred両方に対応しています。


