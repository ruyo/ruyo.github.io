---
title: "もっとPBR背景と合わせる"
---

||
|-|
|[![](./assets/images/small/02s_top2.png)](../assets/images/02s_top2.png)|


----
## モデル製作者への配慮を忘れずに楽しみましょう！

これはモデル製作者が意図していない使い方です。
{: .notice--info}

Toon向けのデータを無理やりPBRに利用します。

モデルは法線やテクスチャをToon向けに加工していたり、アウトラインと合わせてデザインされています。
PBRでの利用はモデル製作者の本意でないことがありますので、ご配慮の上でご利用ください。

## 概要

UE4のサブサーフェスを利用したマテリアルです。素直にライト効果を受けます。

関連するパラメータが多く調整が難しいです。事前に`MToon Lit`での調整を体験してから試すことをオススメします。

やっていることは以下の3つです。
 - 全てのマテリアルをSubsurfaceで作成して色味をあわせる
 - 補助ライトを当てる
 - カラーグレーディングで整える

----
## 下準備をする

新規にレベルを作成し、標準背景(default)を選択します。

ライトやポストプロセスボリュームの些細な違いで調整幅が大きく変わります。
まずは標準背景で特性を掴むことをオススメします。
{: .notice--info}

以下を配置します。

|||
|-|-|
|BP_VrmModelActor|調整対象のキャラクタ|
|CharacterLightRig|キャラライト|
|MaterialUtil|マテリアル調整のメインパネル|
|MToonMaterialSystem|調整補助|
|BP_Bloom|色味が強い特殊なBloom。お好みで|

----
## 背景ライトを整える

ライト設定は重要です！ SSSマテリアルを利用する場合は、必ず以下の項目を確認しましょう。
{: .notice--info}

手順1.
初期配置されているDirectionalLight、SkyLightをMovableにする。

手順2.
各ライトを以下にセットアップする。

DirectionalLight
- CastRaytracingShadows を OFF
  - 陰影を和らげます。レイトレース時のみ影響します。
- DynamicShadowDistanceMovableLight を 3000に設定
  - 近距離の影の精度が上がります。

SkyLight
- LowerHemisphereIsSolidColor を OFF
  - 下方が環境光で照らされます。

設定したらライトをベイクしましょう。エディタ上部のアイコン「Build」の▼をクリックして、「BuildLightingOnly」で完了です。
ベイクしないと、PlayIn中のみ古いライトが参照されます。

----
## SSSモードに切り替える

### キャラクタライトを設定する
CharacterLightRigより、Key、Rimを無効化、AmbientBackを有効化するようチェックボックスを操作します。

||
|-|
|[![](./assets/images/small/02s_light1.png)](../assets/images/02s_light1.png)|


### マテリアルの切り替え
対象のSkeletalMeshをレベルに配置します。
MaterialUtilより、TargetSkeletalMeshActorにそれをセットします。
ボタン `2 PBR SSSMode` をクリックするとマテリアルが切り替わります。

||
|-|
|[![](./assets/images/small/02s_matutil.png)](../assets/images/02s_matutil.png)|

BP_VrmModelActorより、DisableCustomShadowmapをONにします。
最後に`RefreshDummy`をONにします。ここまでの設定がキャラクタに正しく反映されます。チェックボックスは自動でOFFになります。

----
## 調整する 基礎編

### 露出の固定
MaterialSystemより`OverrideExposure`をONにします。調整後に好みによってOFFにしましょう。

調整中に画面全体の明るさが変わってしまうのを抑えます。

||
|-|
|[![](./assets/images/small/02s_ex.png)](../assets/images/02s_ex.png)|


### 色味
MaterialSystemより以下の項目を変更して色味を調整します。
また肌の色味が合わない場合は、MaterialUtilより、SubsurfaceColorで操作します。

ここではやや薄め/暗めに調整しましょう。
後でキャラライトやポストプロセスで補正します。

||
|-|
|[![](./assets/images/small/02s_texpow.png)](../assets/images/02s_texpow.png)|

### ライト
CharacterLightRigより、AmbientBackLightScaleを変更します。ある程度明るさのバランスが取れたらrimを有効化し、輪郭を強調しましょう。

### カラーグレーディング

軽く調整するだけで大きく効果が出ます。のでパラメータを触ってみましょう。

[こちらのオンラインラーニングコース](https://www.unrealengine.com/ja/onlinelearning-courses/creating-photoreal-cinematics-with-quixel)が参考になります。


----
## 調整する 応用編

### 色味・ラフネス個別調整
前述の色味パラメータは、マテリアル毎に変更できます。
同時にラフネスを調整してスペキュラを出すこともできます。

### ライト配置
CharacterLightRigCustomを利用すると、キャラクタ用ライトを自由に追加可能です。慣れたらCustom版で構成しましょう。

|全てCustomで調整した様子。ライト4灯||
|-|-|
|[![](./assets/images/small/02s_light.png)](../assets/images/02s_light.png)|[![](./assets/images/small/02s_custom.png)](../assets/images/02s_custom.png)|

BP_Bloomを利用すると、ハイライト部分に色味を残したBloomがかかり鮮やかになります。お好みでご利用ください。

BP_ColorGradationを利用すると、画面全体にカラーフィルタをかけることができます。上部2隅に色を薄く乗せると雰囲気が出ます。

これらに加えてUE4の機能をフル活用しましょう！

----
## どうしても絵がまとまらないんだけど？

この調整は難しいです。元素材がToon向けであるため、周囲のライティングや元素材の造形・テクスチャによる変化幅が不規則です。

それに加えて、PBRでのライティングやカラーグレーディングのスキルも必要です。

私自身も手探りで調整しています。経験則ですが「顔を補助ライトで照らして中間的な明るさにまとめ、最後にカラーグレーディングで締める」と上手くまとまるようです。

||
|-|
|[![](./assets/images/small/02s_sub.png)](../assets/images/02s_sub.png)|


