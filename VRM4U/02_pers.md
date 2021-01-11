---
title: "魚眼・嘘パースを使う"
---

||
|-|
|[![](./assets/images/small/02p_top2.png)](../assets/images/02p_top2.png)|
|モデル：[NecoMaid PREMIUM](https://sonovr.booth.pm/items/2147201)|

----
## 迫力ある絵を撮りたい

少々扱いにくい機能です。工夫してお使いください。
{: .notice--info}

魚眼レンズのような効果を入れたり、近いものがより大きく見えるような変形をします。
画角が変わったように見えます。

## 魚眼の使い方
CharacterCameraを配置し`UniversalZoom`をONにして画角制限を解除します。
PlayIn後、`Z/Cキー`で画角を調整し、`T/Yキー`で魚眼処理(Paniniプロジェクション)を調整します。

描画負荷が上がるのでご注意ください。魚眼効果中は描画解像度がx2されます。

## 嘘パースの使い方

サンプルマップ `VRM4U_FOV.umap` を参照ください。

`FOVCustom`を配置して`TargetActor`に対象のモデルをセットします。

`FOVCustom` を中心にして、ある距離より離れた箇所がスケールされます。`DistanceFromCamera`で距離を、`FovScale` でスケール値を制御できます。

オプションとして、`CenterBoneName` でアタッチする骨の名前を指定できます。無視しても問題ありません。


|標準|パース補正ON|
|-|-|
|[![](./assets/images/small/02p_p2.png)](../assets/images/02p_p2.png)|[![](./assets/images/small/02p_p1.png)](../assets/images/02p_p1.png)|

----
