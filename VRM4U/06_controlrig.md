---
title: "ポーズを調整する(ControlRig)"
---

||
|-|
|[![](./assets/images/small/06a_top.png)](../assets/images/06a_top.png)|
|モデル：[【オリジナル3Dモデル】サタリナ族のメイドさん](https://booth.pm/ja/items/2589069)|

----
## 概要

VRM4Uが用意したControlRigを対象のモデルに割り当てます。

ControlRigとシーケンサーを利用することで、任意のポージング、アニメーションを作成することができます。

開発中のため、このページの操作手順は、適宜に変更されます。
{: .notice--info}

ControlRigはベータ版であり、適切な公式ドキュメントはありません。情報を参照する際は、対象のバージョンを十分確認ください。(UE4.26現在)
モデルのポージング機能としては十分利用可能です。
複雑な操作時にエディタが停止することがあります。
{: .notice--info}

## 下準備

UE4.26以降で動きます。

以下4つのプラグインを有効化し、エディタを再起動します。
 - Python Editor Script Plugin
 - Control Rig
 - Sequencer Scripting
 - Editor Scripting Utilities

|プラグイン有効化||
|-|-|
|[![](./assets/images/small/06a_p1.png)](../assets/images/06a_p1.png)|[![](./assets/images/small/06a_p2.png)](../assets/images/06a_p2.png)|


有効化後、`/VRM4U Content/Util/Actor/latest` にControlRigのアセットが表示されることを確認します。
また、`WBP_ControlRig`を右クリックから実行し、テンプレート複製UIが起動することを確認します。

||
|-|
|[![](./assets/images/small/06a_ui1.png)](../assets/images/06a_ui1.png)|

|テンプレート複製UIが起動します|
|-|
|[![](./assets/images/small/06a_ui2.png)](../assets/images/06a_ui2.png)|

UI表示でエラーが出る場合は、前述のプラグインが正しく有効化されているか確認ください。

## 手順の要約

 1. テンプレートRigを複製し、SkeletalMeshを差し替える
 1. 複製UIにRigをセットし、Createボタンを押す
 1. Rigを保存し、エディタを再起動する
    - 保存せずにRigをコンパイルしたり操作を継続すると、エディタがクラッシュすることがあります。

テンプレートは3種類あります。通常は `IK Rig` を複製すればOKです。表情を付けたい場合は `Morph Rig` も複製ください。

### IK Rigを作成する

`CR_VRoidSimpleIK`を複製(duplicate)して開きます。

**ControlRig編集画面より**

|複製したControlRigを開いて、、|
|-|
|[![](./assets/images/small/06a_copy0.png)](../assets/images/06a_copy0.png)|


|Rootを選択、Deleteキーを押す（一時的にモデルが崩れます）|
|-|
|[![](./assets/images/small/06a_copy1.png)](../assets/images/06a_copy1.png)|

|モデルを2箇所にセット。「PreviewMesh」 と 「階層右クリック->Import->SelectMesh」|
|-|
|[![](./assets/images/small/06a_copy3.png)](../assets/images/06a_copy3.png)|

モデルは「Import」メニューで更新してください。「Refresh」で更新するとMorphTarget用のアニメーションカーブが変更されません。
{: .notice--info}

**テンプレート複製UIより**
 - 上記設定を行ったControlRigをセット
 - 対象モデルのVrmAssetListをセット

|ControlRigとVrmAssetListをセット|
|-|
|[![](./assets/images/small/06a_copy2.png)](../assets/images/06a_copy2.png)|

`Create IK Rig`ボタンを押し、数十秒待ちます。
完了したらControlRigをSaveし、**念の為エディタを再起動します。**

一度スクリプト実行するとエディタが停止しやすくなります。再起動後は問題なく動作します。
{: .notice--info}

### Morph Rigを作成する

IKテンプレートとほぼ同じ手順で利用できます。

`CR_VRoidSimpleMorph`を複製(duplicate)しモデルを差し替え、複製UIのMorphRigにセットしてCreateしてください。VrmAssetListは不要です。

|MorphRig にセット|
|-|
|[![](./assets/images/small/06a_ui3.png)](../assets/images/06a_ui3.png)|


### FK Rigを作成する

同じく`CR_VRoidSimpleFK` からCreateください。

ただ、現在のFKテンプレートの作成には時間がかかります。骨数が100本を超える場合、 **数分の時間を要します。** 将来的なUE4のバージョンアップにより改善されると思われます。

処理の進行状況をログで確認したい場合、UE4起動時のオプションに`-log`を追加してログウィンドウを表示ください。

```
"C:\Program Files\Epic Games\UE_4.26\Engine\Binaries\Win64\UE4Editor.exe" -log
```

|-log オプションで起動したUE4。スクリプト進行状況が表示される|
|-|
|[![](./assets/images/small/06a_log.png)](../assets/images/06a_log.png)|


----

## シーケンサー操作時に揺れ骨が動くようにする

`PostProcessAnimBlueprint`を利用します。

以下のようなAnimBPを作成し、SkeletalMeshのPostProcessAnimBlueprintにセットすれば完了です。

|作成するAnimBP|SkeletalMeshにセット。プレビューに表示が増える|
|-|-|
|[![](./assets/images/small/06a_post1.png)](../assets/images/06a_post1.png)|[![](./assets/images/small/06a_post2.png)](../assets/images/06a_post2.png)|

----

## 見た目のセットアップを忘れずに！

輪郭線やセルフシャドウを手動で設定する必要があります。[前章の解説を参照ください](../01_look/)