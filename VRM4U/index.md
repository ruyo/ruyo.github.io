---
title: "VRM4U"
share: true
toc: false
classes: wide
---

[![](../assets/images/top_256x256.png)](../assets/images/top_l.png)

----
## VRM4Uとは

UnrealEngine4で動作する、VRMファイルのインポーターです。

[導入はこのリンクから](./01_quick-start/)

[English (GoogleTranslate)](https://translate.google.com/translate?um=1&ie=UTF-8&hl=ja&client=tw-ob&sl=ja&tl=en&u=https%3A%2F%2Fruyo.github.io%2FVRM4U%2F)

----
## 特徴

|||
|:-:|:-:|
|[![](./assets/images/small/03.png)](./assets/images/03.png)|[![](./assets/images/small/04.png)](./assets/images/04.png)|
|[![](./assets/images/small/01_a.png)](./assets/images/01_a.png)|[![](./assets/images/small/01_b.png)](./assets/images/01_b.png)|


スクリーンショットや動画は[**ギャラリーのページ**](./90_gallery/)に沢山あります

 - VRMファイルをインポートできます
 - アニメーション
     - 手軽にリターゲット可能です。A-pose/T-pose、BoneMapが生成されます。
     - 顔アニメ（Morphtarget・BlendShapeGroup）を利用可能です。
     - 揺れ骨にVRMSpringBone、PhysicsAssetを選択できます。
     - 汎用のControlRig、操作用のUMGがあります。
 - マテリアル
     - MToonを再現したマテリアル。影色の指定や、アウトラインの色・太さ調整、MatCapなどが全て適用されます。
     - PBR背景に合わせて描画モードを切り替え・調整できます。
     - 既存のポストフィルタやレイトレースも同時に利用できます。
 - モバイル
     - BoneMapリダクション機能により手軽に表示可能です。
     - 描画クオリティを切り替えできます。ロースペック対応です。
 - VR/AR
     - 描画はForward/Deferred両方に対応しています。
     - シンプルな機能で構成しているため破綻しません。
 - ランタイムロード
     - パッケージング後のEXEファイルから、ユーザの任意のVRMファイルを読み込むことができます。
     - アニメーションはランタイムでリターゲットできます。
 - UE4との相性の良さ
     - インポート後は標準的なSkeletalMeshアセットになります。
     - 対応するUE4のバージョンは4.20~4.26です（2020/12現在）最新版への対応も容易です。

----
## 雰囲気を知りたい

[簡易的ですがYoutubeの動画](https://www.youtube.com/channel/UC9Xuvwk9YLisxtNbTAjryDQ)や、ハッシュタグ[#VRM4U](https://twitter.com/hashtag/VRM4U)を参考にどうぞ

