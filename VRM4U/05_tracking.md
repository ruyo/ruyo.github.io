---
title: "フェイシャルキャプチャ、ハンドトラッキング"
---

----

このドキュメントは書きかけです。

----
## フェイシャルキャプチャ

LiveLinkFaceでキャプチャした表情を、キャラクタに適用します。

LiveLinkFaceが動作するiPhone/iPadが必要です。UE4.25以降で動作します。
{: .notice--info}

以下のサンプルマップを参照してください。UE4.25以降でのみコンテンツブラウザに表示されます。

Maps/latest/VRM4U_LiveLinkFace

端末にてLiveLinkFaceを起動し顔を認識させます。
うまく動作していれば、以下のように端末が認識されます。

表示される項目は端末によって異なると思います。

||
|-|
|[![](./assets/images/small/05t_live.png)](../assets/images/05t_live.png)|

端末が認識されたら、BP_LiveLinkFaceにセットします。
認識されていない場合はリストに表示されません。

||
|-|
|[![](./assets/images/small/05t_sub.png)](../assets/images/05t_sub.png)|

PlayInで動きます。

認識されない場合は設定を確認ください
- エディタの設定
  - プラグイン`AppleARKitFaceSupport`を有効にする
- 端末の設定
  - `設定 > livelink > ターゲット` にエディタ起動しているPCのIPアドレスを記入する
  - 例えば「192.168.1.---:11111」のように。(---には実際のPCのアドレスから数値を入れてください)

----
## キャラクタ毎にカスタマイズする

BP_LiveLinkFaceをコピーして、カスタマイズして利用ください。

- VRoidモデル
  - そのままである程度動作します。
- その他フルスクラッチのモデル
  - VRMのBlendShapeGroupに登録された表情のみ動きます。

任意の表情を利用したい場合はノードを改変してください。
未整理ですみません…

||
|-|
|[![](./assets/images/small/05t_detail.png)](../assets/images/05t_detail.png)|


## ハンドトラッキング（上級者向け）

OculusQuestで認識した手指を、キャラクタに適用します。

OculusQuestが必要です。PCにOculusLinkで接続します。
{: .notice--info}

Oculus社が公開しているUE4が必要です。githubよりダウンロードしエディタビルドする必要があります。
{: .notice--info}

### エディタをビルドする
[こちらのgithubより、UE4.25をダウンロードします。](https://github.com/Oculus-VR/UnrealEngine)

[ビルドのセットアップは こちらを参照ください。](https://qiita.com/ruyo/items/08ac751ba61cb1201e96)

### VRM4Uよりトラッキングを有効化する

`VRM4U.Build.cs`にて、`bUseQuestTracking = true`　としてください。

### ハンドトラッキングする

以下のサンプルマップを利用ください。VRPreviewすると、頭と手が動きます。

Maps/VRM4U_Tracking

