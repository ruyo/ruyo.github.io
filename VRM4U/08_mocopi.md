---
title: "モーションキャプチャ(mocopi UDP)を受け取る"
---

||
|-|
|[![](./assets/images/small/08a_m5.png)](../assets/images/small/08a_m5.png)|
|モデル：UE5マネキン|

----

## 概要

外部アプリからモーションキャプチャデータを受け取り、モデルにアニメーションを適用します。

[mocopi公式サイト](https://www.sony.jp/mocopi)

[mocopi開発者向け情報](https://www.sony.net/Products/mocopi-dev/jp/documents/Home/TechSpec.html)

----

## mocopi UDP を受け取る

サンプルマップ `VRM4U_Mocopi` を参照ください

レベル上のBP_MocopiReceiverにポート番号を設定後、Listenボタンを押すかPlayInしてください。

|[![](./assets/images/small/08a_m1.png)](../assets/images/small/08a_m1.png)|

完了です。

アニメーションは ABP_VRoidMocopi_Bone を参照ください。
VRMのHumanoidBoneに流し込んでいるだけです。シンプルです。

## mocopi BVH をインポートする

UE5.1以降での作業をオススメします。リターゲットが容易です。
{: .notice--info}

[BVHインポート方法はこちら](../04_bvh/)

インポート時に、BVHモデルのAポーズ用アセットと、リターゲット用IKRIGアセットが生成されます。

### VRMモデルにリターゲット

インポート時に生成されているそれぞれのIKRIGを利用し、IKRetargeterを作成してください。

そのまま（Tポーズのまま）リターゲット可能です。

### UE5マネキンにリターゲット

IKRetargeterを作成します。
例えばモデル名がSampleである場合、インポート時に IK_Sample_Mannequin というIKRigが生成されます。これをベースにIKRetargeterを作成し、ターゲットを UE5マネキンのIKRIG(サードパーソンテンプレートに含まれているもの)に指定します。

UE5.1以降を利用している場合、リターゲット元の姿勢をAポーズに設定できます。
以下のようにBVH側がAポーズになります。

|初期状態|Aポーズ設定後|
|-|-|
|[![](./assets/images/small/08a_m4.png)](../assets/images/small/08a_m4.png)|[![](./assets/images/small/08a_m2.png)](../assets/images/small/08a_m2.png)|

自動設定されたChainMappingには不要な設定が含まれており、指先や肘・膝が捻れています。
解消するために、指先やTwistBoneの設定を下図のように「None」に設定ください。

|不必要なChainMappingをNoneに設定|
|-|
|[![](./assets/images/small/08a_m3.png)](../assets/images/small/08a_m3.png)|

完了です。

----

## 詳細解説（UEの操作に慣れてる人向け）

### 揺れ骨を適用する

揺れ骨を適用する場合は`VRMSpringBone`ノードも追加ください。
[揺れ骨の解説はこちら](../01_animation/)

### 複数の外部アプリからのデータ受信

レベルに各種Receiverをを複数配置し、ポート番号を設定ください。それぞれデータが受信されます。

データの参照には、`VRM4U_AnimationSubsystem`へのアクセス時に、「ポート番号指定」または「通し番号指定」を利用してください。
