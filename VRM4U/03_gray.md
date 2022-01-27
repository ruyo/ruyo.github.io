---
title: "グレイマンを置き換える"
---

||
|-|
|[![](./assets/images/small/03a_top.png)](../assets/images/03a_top.png)|
|モデル：[ミライ小町](https://www.bandainamcostudios.com/works/miraikomachi/dlcguideline.html)|

----

## 概要

グレイマンをVRMモデルに置き換える手法を紹介します。
2つのアプローチがあります。

 - 手法その１：リアルタイムリターゲット（VRM4U独自機能）
   - レベル上で動いているグレイマンのアニメーションを、直接VRMモデルに割り当てます。
   - 良い点：圧倒的に簡単。
   - 悪い点：微調整できない。厳密なコリジョンや接地感を出すことが難しい。
 - 手法その２：オフラインリターゲット（UE標準機能）
   - リターゲットマネージャでAnimSequenceを複製したり、AnimBPを作成します。
   - 良い点：標準機能なので安心。細かく調整できる
   - 悪い点：圧倒的に手間がかかる。特にAnimBPが複雑な場合は組み直しが大変。骨向きの補正が難しい

具体的な手順を解説後、ユースケースを紹介します。

----

## リアルタイムリターゲットする（VRM4Uの機能）

### モデルをレベルに配置して利用する

`BP_VrmMannequinRetarget` を配置し、`Targetmannequin` にコピー元となるグレイマンを指定します。他モデルでも、グレイマンと同じ骨名であればOKです。

PlayInすると、VRM標準モデルにリターゲットされます。完了です。

|TargetMannequinをセットして、、|PlayInで動く|
|-|-|
|[![](./assets/images/small/03r_set1.png)](../assets/images/03r_set1.png)|[![](./assets/images/small/03r_set2.png)](../assets/images/03r_set2.png)|


モデルを差し替えるには、VrmAssetListOverride にアセットを設定します。
`GenerateRegargetPoseCopy` ボタンを押すと、エディタ上にプレビューモデルが生成されます。

|VrmAssetListOverrideをセット、ボタンを押すとプレビュー表示|PlayInで動く|
|-|-|
|[![](./assets/images/small/03r_setM1.png)](../assets/images/03r_setM1.png)|[![](./assets/images/small/03r_setM2.png)](../assets/images/03r_setM2.png)|
|モデル：[【オリジナル3Dモデル】ドラゴニュート・シェンナ](https://booth.pm/ja/items/2661189)||


**選択するActorに注意ください。** リターゲット設定は `BP_VrmMannequinRetarget` で操作します。プレビューモデルをクリックすると、子Actorである `BP_VrmPoseCopy` が選択されます。
{: .notice--info}
| **注意！** モデルをクリックすると `BP_VrmPoseCopy` が選択される。これはモデルActor。**リターゲットはその親Actorで設定する**|
|-|
|[![](./assets/images/small/03r_pose.png)](../assets/images/03r_pose.png)|

### モデルをSpawnして利用する

差し替え対象のActorの中で `BP_VrmMannequinRetarget` を作成、初期化ノードを呼び出してください。

|ChildActorとしてセットし、BeginPlayで初期化、元モデルを表示OFFにする|PlayInで置き換わる|
|-|-|
|[![](./assets/images/small/03r_swap.png)](../assets/images/03r_swap.png)|[![](./assets/images/small/03r_swap2.png)](../assets/images/03r_swap2.png)|


### リアルタイムリターゲット 応用編

モデルにオブジェクトをアタッチする場合は、`BP_VrmPoseCopy`を利用します。

レベル配置の場合は、そのままActorにアタッチしてください。
Spawnしている場合は、`BP_VrmMannequinRetarget` より、関数 `GetRetargetSkeletalMeshComponent` で対象を取得できます。

MorphTargetを設定する際も同様です。

|モデルのアタッチやMorphTargetの設定は BP_VrmPoseCopyを利用する|
|-|
|[![](./assets/images/small/03r_attach.png)](../assets/images/03r_attach.png)|

アウトラインと揺れ骨は自動設定されます。それぞれオプションで無効化できます。

----

## UE4標準機能でリターゲットする

### Advanced Locomotion System に適用する

[Advanced Locomotion System](https://www.unrealengine.com/marketplace/en-US/product/advanced-locomotion-system-v1)に適用するチュートリアルビデオがあります。

{% include video id="fsP68yQHIbs" provider="youtube" %}

以下、動画の要所を解説します。

----
### スケルトンをUE4の骨名で作成する

インポート時に`HumanoidMesh`と`IKBone`にチェックを入れます。

骨名が変わるだけです。骨の向きは変化しません。
{: .notice--info}

VRMモデルとグレイマンのSkeleton共通化は、正しく動作しません。
{: .notice--info}


||
|-|
|[![](./assets/images/small/03a_import.png)](../assets/images/03a_import.png)|

メッシュが3つ出力されます。それぞれ骨名の命名規則が異なります。

|種類|用途|
|-|-|
|モデル骨名|ほとんどの場合これでOKです。モデルの骨名を利用します。よくわからない場合はこれ|
|グレイマン命名規則|グレイマン用に組まれた複雑なシステムを流用する場合|
|VRM命名規則|滅多に使わない。複数のVRMをターゲットにした複雑なシステムを構築する場合|

Humanoidの骨が以下のような名前になります。それぞれにIKBoneも追加されます。

|左：モデル骨名、中央：VRM命名規則、右：グレイマン命名規則|
|-|
|[![](./assets/images/small/03a_bone.png)](../assets/images/03a_bone.png)|

----
### VirtualBone、Socketを複製する

`AssetUtil` を利用して、既存のSkeletalMeshからVirtualBoneとSocketを複製することができます。
対象はHumanoid骨の子供だけです。

VirtualBoneでIKを制御したり、Socketで武器をアタッチするためのものです。

Socketはプレビューで位置が異なるように見える場合がありますが、問題ありません。初期姿勢がA-pose/T-poseで異なる影響です。同じポーズをとった時に座標が一致します。
{: .notice--info}


||
|-|
|[![](./assets/images/small/03a_bone2.png)](../assets/images/03a_bone2.png)|

----
### PhysicsAssetを複製する

`AssetUtil` を利用して、既存のSkeletalMeshからPhysicsAssetを複製することができます。
対象はHumanoid骨についているコリジョンだけです。

ラグドールの下地として有用です。

コリジョンの回転は反映されません。骨の軸向きを補正できないためです。正確に当てはめる場合は手動で調整ください。
{: .notice--info}

|元データ|VRMモデルにコピーしたもの|
|-|-|
|[![](./assets/images/small/03a_bone3.png)](../assets/images/03a_bone3.png)|[![](./assets/images/small/03a_bone4.png)](../assets/images/03a_bone4.png)|


----
### 最後の仕上げを忘れずに

輪郭線や影を反映させましょう。キャラクタのBlueprintにMToonAttachActorをアタッチすればOKです。

揺れ骨を正確に動かしましょう。AnimBlueprintの最後に `VRMSpringBone`ノードを追加すればOKです。

リターゲットの結果が変な場合は、SkeletonのA-pose/T-poseを確認してください。


||
|-|-|
|[![](./assets/images/small/03a_sword.png)](../assets/images/03a_sword.png)|


----

## 総括

リアルタイムリターゲットの手軽さが光りますね！

…とはいえ厳密な調整には向かないため、用途に応じて手法を使い分けください。
以下に状況別で紹介します。

 - リアルタイムリターゲット向き
   - メインキャラクターをUE4Mannequin準拠で作成している
   - 既にグレイマンを用いて、ある程度の規模のゲームが動作している
   - 試しにキャラクタをVRMモデルに差し替えてみたい。オマケでVRM対応したい
 - オフラインリターゲット向き
   - メインキャラクターをVRMモデルで作成している
   - 厳密な当たり判定、インタラクションが必要である

## おまけ

PMXモデルに対するリアルタイムリターゲットも可能です。`BP_VrmMannequinRetarget` のオプションを設定ください。

||
|-|
|[![](./assets/images/small/03r_pmx.png)](../assets/images/03r_pmx.png)|
|モデル：[初音ミク by む～ぶさん](https://piapro.jp/t/0Hwp)|
