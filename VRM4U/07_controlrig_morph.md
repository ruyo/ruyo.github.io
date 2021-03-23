---
title: "表情を制御する(ControlRig)"
---

||
|-|
|[![](./assets/images/small/07a_top.png)](../assets/images/07a_top.png)|
|モデル：[【オリジナル3Dモデル】ドラゴニュート・シェンナ](https://booth.pm/ja/items/2661189)|

----
## 概要

シーケンサーを利用し、MorphTargetのアニメーションを作成します。

IKRigと併用する場合、シーケンサーへの登録順をMorphRig > IKRigにする必要があります。サンプルマップ VRM4U_ControlRig を参考にしてください。
{: .notice--info}

ここで紹介するMorph用の機能は どんなSkeletalMeshにも利用できます。FBXとしてインポートしたモデルも動作します。

## 下準備

[前述の解説より](../06_controlrig/)、`Morph Rig` を作成ください。

続いて `WBP_MorphTarget`を右クリックから実行し、MoprhTarget制御UIを起動します。

||
|-|
|[![](./assets/images/small/07a_ui1.png)](../assets/images/07a_ui1.png)|

|Morph制御UIが起動します|
|-|
|[![](./assets/images/small/07a_ui2.png)](../assets/images/07a_ui2.png)|

## 操作手順

 1. MorphRigをレベルに配置し、シーケンサーの編集モードに入る
 1. 制御UIより、操作対象のモデルをTargetActorに設定する
 1. MorphTargetを制御しキーを打つ。

|TargetActorより対象のモデルを選択する|
|-|
|[![](./assets/images/small/07a_ui3.png)](../assets/images/07a_ui3.png)|

|シーケンサーより対象のTrackを選択し、「AddKey」ボタン or 「K」キー|
|-|
|[![](./assets/images/small/07a_ui4.png)](../assets/images/07a_ui4.png)|

## 細かい機能紹介

 - ショートカットキー
   - k  キー追加
   - i  パラメータ初期化
 - Morph名フィルタ
   - 上部のテキスト入力欄でMorph名をサーチできます
 - 不要キーの省略
   - 差分がtolerance以下の場合、キー追加をスキップします
 - 長いMorph名の省略
   - Morph名の先頭を省略します。TargetActorのRemoveStringに一致したものが対象です

## 細かい仕組み（中身を知りたい方向け）

複製スクリプトによって、ControlRigにMorphTarget数ぶんのControlを追加しています。それらの値をカーブ値に渡しています。

あとはシーケンサーでControlの値を変更すれば、MorphTargetへ反映されます。お手軽です。

