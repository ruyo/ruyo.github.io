---
title: "フォトモードTips"
---


----
## カメラ操作

|効果|入力方法|
|-|-|
|移動：前後左右|w a s d|
|移動：上下|q e|
|ズーム変更|z c （xで初期値）|
|ピント調整|shift+z shift+c （shift+xで初期値）|
|ロール回転|1 3 （2で初期値）|
|ピッチ、ヨー回転|マウス前後左右|

エディタ上で直接CineCameraを回転して調整することも可能です。

|ロール回転|縦|
|-|-|
|[![](./assets/images/small/02g_roll.png)](../assets/images/02g_roll.png)|[![](./assets/images/small/02g_roll2.png)](../assets/images/02g_roll2.png)|
|モデル：[NecoMaid](https://booth.pm/ja/items/1843586) （fbx -> VRM変換）||

----
## 顔に落ちる影を消したい

|初期状態|対応後（影対応あり）|
|-|-|
|[![](./assets/images/small/02g_shadow2.png)](../assets/images/02g_shadow2.png)|[![](./assets/images/small/02g_shadow1.png)](../assets/images/02g_shadow1.png)|
|モデル：[ヴィクトリア・ルービン](https://hub.vroid.com/characters/2792872861023597723/models/5013769147837660446)||


マテリアルパラメータで制御可能です。`mtoon_ReceiveShadowRate`を0にしてください。
これはMToonの機能です。

||
|-|
|[![](./assets/images/small/02g_shadow3.png)](../assets/images/02g_shadow3.png)|

またセルフシャドウ自体を無効化して対応することも可能です。


----
## 顔色が悪い/暗いのを修正したい

|初期状態。SSAO 強め|対応後（SSAO なし）|
|-|-|
|[![](./assets/images/small/02g_ssao1.png)](../assets/images/02g_ssao1.png)|[![](./assets/images/small/02g_ssao2.png)](../assets/images/02g_ssao2.png)|
|モデル：[千駄ヶ谷 篠](https://hub.vroid.com/characters/5860098757548846785/models/648876553405728395)||


大抵はSSAOの影響です。対応方法をオススメ順に紹介します。

|対応方法|補足|
|-|-|
|レイトレースAOを利用する|見栄えは良い。ただし描画負荷は高い|
|SSAOを弱める/無効化する|絵が寂しい|
|ライトを明るくする|解決できるか状況による|

レベル上にPostProcessVolumeが配置されていることを確認してから、
`MToonMaterialSystem`よりSSAOを弱めてください。全体の明るさも調整可能です。


----
## マッハバンドを消したい＆色が濃いのを修正したい

|初期状態|対応後（色再現モードON）|
|-|-|
|[![](./assets/images/small/02g_color2.png)](../assets/images/02g_color2.png)|[![](./assets/images/small/02g_color1.png)](../assets/images/02g_color1.png)|
|モデル：[ノワ](https://booth.pm/ja/items/1859878)||

色再現モードを利用することで、なだらかなグラデーションや淡い色の再現が可能です。
`MToonMaterialSystem` より切り替えます。
画面全体の色合いが大きく変わるため、背景と合わせて確認ください。


### 色再現モードの細かい話
VRM4Uのデフォルトマテリアルはマッハバンド（不連続なグラデーション）や色ズレが出やすいです。これはUE4標準のFilmicTonemapperを逆変換してテクスチャ原色を出しているためです。

色再現モードで行っていることは2つです。Tonemapモードの切り替えと、マテリアルの逆変換処理のスキップです。マッハバンドは解消されますが、画面全体の色合いが大きく変わります。

さらに厳密に色再現したい場合はTonemapを無効化してください。ただしポストフィルタの効果（被写界深度やカラーグレーディングなど）がなくなります。無効化時は影響範囲を十分ご確認ください。

