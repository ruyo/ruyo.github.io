---
title: "アニメーションをリターゲット、揺れ骨を再現する"
---

||
|-|
|[![](./assets/images/01c_top.png)](../assets/images/01c_top.png)|


----
## リターゲットする

UE4標準の方法で可能です。セットアップの大半は自動化されています。

[こちらの公式ドキュメントの後半](https://docs.unrealengine.com/ja/Engine/Animation/AnimHowTo/Retargeting/index.html)より、「Retarget Anim Assets -> Duplicate Anim Assets and Retarget」以降の項目を参照ください。


A-poseとT-poseの違いに注意ください。
具体的に以下のような場面は切り替えが必要です。

|正しい組み合わせ|間違った組み合わせ|
|-|-|
|[![](./assets/images/01c_reta.png)](../assets/images/01c_reta.png)|[![](./assets/images/01c_rett.png)](../assets/images/01c_rett.png)|




VRM4Uアセットはポーズを切り替え可能です。
以下よりポーズを指定してください。

||
|-|
|[![](./assets/images/01c_ta.png)](../assets/images/01c_ta.png)|

A-Tを切り替え可能です。

|A-pose|T-pose|
|-|-|
|[![](./assets/images/01c_a.png)](../assets/images/01c_a.png)|[![](./assets/images/01c_t.png)](../assets/images/01c_t.png)|


補足です。標準のTPSテンプレートののグレイマンはリターゲット設定がありません。これを利用する場合は下図のように`Humanoid`を選択してください。（前述の公式ドキュメント前半と同じ手順です）

||
|-|
|[![](./assets/images/01c_gray1.png)](../assets/images/01c_gray1.png)|

----

## 揺れ骨を再現する

**初期状態では揺れ骨が再現できていません。**
PhysicsAssetである程度再現していますが不完全です。

ここではVRMSwingBoneを再現します。AnimBlueprintにノードを追加します。

`SkeletalMesh`より、`AnimBlueprint`を作成します。

||
|-|
|[![](./assets/images/01c_anim1.png)](../assets/images/01c_anim1.png)|


ノードの最後に`VRMSprintBone`を追加し、対象キャラクタの`VRMMetaObject`をセットします。

||
|-|
|[![](./assets/images/01c_anim2.png)](../assets/images/01c_anim2.png)|

`PhysicsAsset`による揺れ骨を無効化します。SkeletalMeshより`PhysicsAsset`の欄で `clear` を選択し空欄にします。

||
|-|
|[![](./assets/images/01c_anim3.png)](../assets/images/01c_anim3.png)|

VRMの設定値で揺れました。

||
|-|
|[![](./assets/images/01c_anim4.png)](../assets/images/01c_anim4.png)|

揺れが大きい場合は `VRMSprintBone` のパラメータで調節可能です。

UE4でアクションさせる場合は `StiffnessScale` を2～3あたりに設定すると安定しやすいです。

多くのVRMファイルは、アバターとしてモーションキャプチャを適用した時に適切に揺れるよう調整されています。アクションゲームのアニメーションを適用すると、揺れ方がオーバーに見えることがあります。


||
|-|
|[![](./assets/images/01c_anim5.png)](../assets/images/01c_anim5.png)|

