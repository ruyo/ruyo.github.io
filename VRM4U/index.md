---
title: "VRM4U"

gallery:
  - url: /VRM4U/assets/images/010_top.png
    image_path: /VRM4U/assets/images/010_top.png
---

## はじめに
VRM4UはVRMファイルのインポーター兼ランタイムローダーです

## 特徴

|||
|----|----|
|![](/assets/images/03.png)|![](/assets/images/04.png)|
|![](/assets/images/01.png)|![](/assets/images/02.png)|


 - VRMファイルをインポートできます。
 - アニメーション
     - 骨、Morphtarget・BlendShapeGroup、揺れ骨・コリジョン などが生成されます。
     - 揺れ骨の挙動はVRMSpringBoneかPhysicsAssetを選択できます。
     - Humanoid用のRIGが生成されるので、アニメーションを手軽にリターゲット可能です。
 - マテリアル
     - MToonを再現したマテリアル。影色の指定や、アウトラインの色・太さ調整、MatCapなど一通り適用されます。
     - 既存のPBR背景の中にキャラクタを描画できます。ポストプロセスを利用しません。
 - モバイル
     - BoneMapリダクションを使うことで、公式のUE4エディタからモバイルでSkeletalMeshを利用できます。
     - 描画はForward/Deferred両方に対応しています。