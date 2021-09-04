---
title: "ControlRigでポーズ・フェイシャルを制御する"
---

||
|-|
|[![](./assets/images/small/07a_top.png)](../assets/images/07a_top.png)|
|モデル：[【オリジナル3Dモデル】ドラゴニュート・シェンナ](https://booth.pm/ja/items/2661189)|
|ボディアニメーション：[Control Rig Mannequinサンプル](https://www.unrealengine.com/marketplace/en-US/product/control-rig-mannequin) からIKRigにベイクして編集|
|フェイシャルアニメーション：MorphRigによる手付け|


----

## 概要

ControlRigとシーケンサーを利用し、姿勢や表情のアニメーションを作成します。

Rigを複数利用する場合、特別なセットアップが必要です。ページ後半を参照ください。
{: .notice--info}

## 下準備

[前述の解説より](../06_controlrig/)、`IKRig`と`MorphRig` を作成ください。

サンプルマップ `VRM4U_ControlRig` も参考にどうぞ。

----

## ポーズ・アニメーションの設定

### ポーズ、アニメーションを作成する

`IKRig`をコンテンツブラウザからレベルに配置します。自動的にシーケンサー編集モードになります。他の手順でも構いません。

コントローラを操作するとキャラクタが動きます。アニメーションを作成する場合は、シーケンサーにキーを追加します。

||
|-|
|[![](./assets/images/small/07a_pose2.png)](../assets/images/07a_pose2.png)|

### 既存アニメーションを編集する

既存アニメーションを、ControlRigの動きにベイクし、再編集することができます。（RigにはBackwardSolveを設定済です）

アプローチは2つあります。

|概要|詳細|
|-|-|
|(オススメ)<br>加算アニメで調整する|toleranceを小さめにベイクし、additiveセクションを追加。オフセットを入れて制御する|
|初期設定で調整する|初期設定でベイクし、コントローラを制御する。細かい動きが再現されない|

|アニメーションをセットしてtoleranceを小さめにベイク|
|-|
|[![](./assets/images/small/07a_pose3.png)](../assets/images/07a_pose3.png)|

|additiveセクションを追加|additive側にキーを打つと既存アニメを調整できる|
|-|-|
|[![](./assets/images/small/07a_pose1.png)](../assets/images/07a_pose1.png)|[![](./assets/images/small/07a_pose4.png)](../assets/images/07a_pose4.png)|


----

## 手首のねじれ補正を調整する

初期状態で軽く補正が入っています。好みに応じて調整ください。

|手首ねじれ補正コントローラ|補正ON（初期0.3）|補正OFF（0.0）|
|-|-|-|
|[![](./assets/images/small/06a_hand.png)](../assets/images/06a_hand.png)|[![](./assets/images/small/06a_hand_on.png)](../assets/images/06a_hand_on.png)|[![](./assets/images/small/06a_hand_off.png)](../assets/images/06a_hand_off.png)|

----

## 表情の設定

IKRigとMorphRigを併用する場合は、後述のセットアップも合わせて参照ください。
{: .notice--info}

`WBP_MorphTarget`を右クリックから実行し、MoprhTarget制御UIを起動します。

||
|-|
|[![](./assets/images/small/07a_ui1.png)](../assets/images/07a_ui1.png)|

|Morph制御UIが起動します|
|-|
|[![](./assets/images/small/07a_ui2.png)](../assets/images/07a_ui2.png)|

### 表情：操作手順

 1. MorphRigをレベルに配置し、シーケンサーの編集モードに入る
 1. 制御UIより、操作対象のモデルをTargetActorに設定する
 1. MorphTargetを制御しキーを打つ。

|TargetActorより対象のモデルを選択する|
|-|
|[![](./assets/images/small/07a_ui3.png)](../assets/images/07a_ui3.png)|

|シーケンサーより対象のTrackを選択し、「AddKey」ボタン or 「K」キー|
|-|
|[![](./assets/images/small/07a_ui4.png)](../assets/images/07a_ui4.png)|

### 表情：細かい機能紹介

 - ショートカットキー
   - k  キー追加
   - i  パラメータ初期化
 - Morph名フィルタ
   - 上部のテキスト入力欄でMorph名をサーチできます
 - 不要キーの省略
   - 差分がtolerance以下の場合、キー追加をスキップします
 - 長いMorph名の省略
   - Morph名の先頭を省略します。TargetActorのRemoveStringに一致したものが対象です
 - エラー検知
   - エラー時はボタンの色が変わります。シーケンサーより対象のTrackを選択して再度キーを追加してください。

|ボタンが赤い時はエラー。シーケンサーより対象のTrackを選択する|
|-|
|[![](./assets/images/small/07a_ui5.png)](../assets/images/07a_ui5.png)|

### 表情：細かい仕組み（中身を知りたい方向け）

複製スクリプトによって、ControlRigにMorphTarget数ぶんのControlを追加しています。それらの値をカーブ値に渡しています。

あとはシーケンサーでControlの値を変更すれば、MorphTargetへ反映されます。お手軽です。

この仕組みはVRMに依存していないため、どのようなSkeletalMeshにも適用できます。FBXインポートしたものにも使えます。


----

## 複数のRigを同時に利用する

**標準的な作業手順では問題が出ます！** Rigを複数利用する場合は十分ご確認ください。正しくセットアップしたものは サンプルマップ VRM4U_ControlRig で確認できます。
{: .notice--info}

以下の図のような手順でRigを複数設定します。

||||
|-|-|-|
|[![](./assets/images/small/07a_set1.png)](../assets/images/07a_set1.png)|[![](./assets/images/small/07a_set2.png)](../assets/images/07a_set2.png)|[![](./assets/images/small/07a_set3.png)](../assets/images/07a_set3.png)|


### 正しい構成

以下の画像のようにセットアップされていれば問題ありません。

|Rigの登録場所に注意！！|
|-|
|[![](./assets/images/small/07a_r1.png)](../assets/images/07a_r1.png)|

```
正しい構成
-SkeltalMeshActor
  -SkeletalMeshComponent0   <- 「+Track」をクリックして追加
    -IK_Rig           <- OK.  ここがIKRig
  -Morph_Rig          <- OK.  ここがMorphRig
```

### 問題ある構成

標準的な作業手順では、以下のような構成になりやすいです。

```
問題ある構成
-SkeltalMeshActor
  -SkeletalMeshComponent0
    -Morph_Rig       <- NG.  MorphRigとIKRigが逆
  -IK_Rig            <- NG. 
```

この構成、一見正しく動作しますが、**`IKRig`を選択した時にシーケンサのフォーカスが移動しません！**
キーを打つ手間が大変かかります。

修正には 以下のように操作します。

|IKRigを2つ登録して、キーを選択、移動先のrigにコピーする|
|-|
|[![](./assets/images/small/07a_r2.png)](../assets/images/07a_r2.png)|

キーを移動後、元の`IKRig`を削除し 改めて`MorphRig`を追加すれば完了です。

----

## シーケンサー操作時に揺れ骨が動くようにする

`PostProcessAnimBlueprint`を利用します。

以下のようなAnimBPを作成し、SkeletalMeshのPostProcessAnimBlueprintにセットすれば完了です。

|作成するAnimBP|SkeletalMeshにセット。プレビューに表示が増える|
|-|-|
|[![](./assets/images/small/06a_post1.png)](../assets/images/06a_post1.png)|[![](./assets/images/small/06a_post2.png)](../assets/images/06a_post2.png)|


----


## 見た目のセットアップを忘れずに！

`MToonAttachActor`を配置してTargetをセットしてください。輪郭線やセルフシャドウが有効化されます。
[詳しくは前章の解説を参照ください](../01_look/)


----
----

## 補助骨が動くようにする（上級者向け）

補助骨用のControlRigをセットアップし、PostProcessAnimBlueprint にセットすれば完了です。

モデルに補助骨が設定されていると効果的です。無い場合は親骨を指定しても構いません。また前段のねじれ補正はOFFにしてください。
{: .notice--info}

手順は以下です。

 - `CR_HelperBone`を複製し、Import Hierarchy で対象のモデルを指定
 - パラメータを書き換える
   - 動かしたい補助骨とその連動元、ブレンド率などを設定
 - AnimBPにセット

|モデルを指定|パラメータセットアップ|AnimBP設定|
|-|-|-|
|[![](./assets/images/small/06a_helper1.png)](../assets/images/06a_helper1.png)|[![](./assets/images/small/06a_helper2.png)](../assets/images/06a_helper2.png)|[![](./assets/images/small/06a_helper3.png)](../assets/images/06a_helper3.png)|

動作確認にはControlRigやSkeletonのプレビューを利用ください。

|補助骨設定 あり|補助骨設定 なし|
|-|-|
|[![](./assets/images/small/06a_helper_on.png)](../assets/images/06a_helper_on.png)|[![](./assets/images/small/06a_helper_off.png)](../assets/images/06a_helper_off.png)|


----

## マテリアルパラメータのアニメーションを適用する（上級者向け）

サンプルマップ`VRM4U_BlendShapeGroup.umap`を参照ください。

`BP_BlendShapeGroupController` から設定可能です。VRMのBlendShapeGroupで指定したMorphとMaterialListが適用されます。

|マテリアルパラメータ指定|
|-|
|[![](./assets/images/small/06a_mat.png)](../assets/images/06a_mat.png)|

