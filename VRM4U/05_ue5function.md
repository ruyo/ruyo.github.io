---
title: "UE5専用機能"
---


----

## (SubsurfaceProfile) 影にポリゴン形状が出るのを抑える

UE5は非常に細かいポリゴンに向けて調整されているため、モデルによってはキレイな影が出ません。

それを改善するパラメータです。

|初期状態|NormalBias調整後（オススメ）|従来のShadowmap|
|-|-|-|
|[![](./assets/images/small/05u_s1.png)](../assets/images/05u_s1.png)|[![](./assets/images/small/05u_s2.png)](../assets/images/05u_s2.png)|[![](./assets/images/small/05u_s3.png)](../assets/images/05u_s3.png)|
|ポリゴンのエッジに沿った影が出てしまう|←を改善したもの。<br>影をぼかしたい場合はライト側のパラメータで設定する|影の解像度が低い。全体的にぼけてしまう|
|モデル：[NecoMaid RICH](https://booth.pm/ja/items/2147191)||



### 仕組み

コンソールコマンド r.Shadow.Virtual.NormalBias を利用しています

くわしく知りたい方は こちらを参照ください。

[https://docs.unrealengine.com/5.0/en-US/virtual-shadow-maps-in-unreal-engine/](https://docs.unrealengine.com/5.0/en-US/virtual-shadow-maps-in-unreal-engine/)

## (MToonUnlit) 色味を完全に再現する

UEはFilmicTonemapperの影響で、テクスチャの色味を再現できません。

その影響度合いを調整するパラメータです。
同時に、VRM4Uで行っている逆変換の強さも調整できます。

背景も含めて色味が変わるため、フォトリアリスティックな表現には向きません。厳密な色再現が必要な場合に、状況に応じて利用ください。

|初期状態|色再現したもの|（参考）再現したいテクスチャの色|
|-|-|-|
|[![](./assets/images/small/05u_c1.png)](../assets/images/05u_c1.png)|[![](./assets/images/small/05u_c2.png)](../assets/images/05u_c2.png)|[![](./assets/images/small/05u_c3.png)](../assets/images/05u_c3.png)|
|少し色味がずれてしまう。逆変換で補正しきれない|テクスチャの色が適用される。<br>ただし背景にも影響してしまう。影響度を調整できる|（参考）この色が再現できればOK|


### 仕組み

PostProcessVolumeのToneCurveAmountパラメータを利用しています。
従来この影響度合いはON/OFFでのみ切り替え可能でした。興味ある方は[Tipsページのマッハバンド対策を参照ください。](../02_shortcut2/)
