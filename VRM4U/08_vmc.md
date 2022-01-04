---
title: "モーションキャプチャ(VMC Protocol)を受け取る"
---

||
|-|
|[![](./assets/images/small/08a_top.png)](../assets/images/08a_top.png)|
|モデル：VRoidStudio プリセット組み合わせ|

----

## 概要

外部アプリからモーションキャプチャデータを受け取り、モデルをアニメーションさせます。

Virtual Motion Capture Protocol（以下VMC Protocol）の解説は[こちら](https://protocol.vmc.info/)


この機能はタフな動作チェックを行っていません。
VMC対応については、はるくさん開発のVMC4UEの利用もご検討ください。
https://github.com/HAL9HARUKU/VMC4UE
{: .notice--info}

----

## 下準備

サンプルマップ `VRM4U_VMC` を参考に設定ください。

動作にはEpic公式の`OSCプラグイン`が必要です。有効化し、エディタを再起動ください。

||
|-|
|[![](./assets/images/small/08a_plugin.png)](../assets/images/small/08a_plugin.png)|


**UE5EA版では大きな不具合が2つあります。**
いずれも**UE5正式版では修正される**予定です。
なおUE4では問題なく利用可能です。
{: .notice--info}

 - 不具合1: UE5EAはOSCバンドルを受信できません
   - 送信元アプリ側で通信設定を変更可能であれば、切り替えて利用ください。
 - 不具合2: UE5EAは後述のBlendShapeやトラッカーを正しく検索できないことがあります
   - MapのFindが正しく動作しません。呼ばないよう組み替えてください。Blurprint/cppどちらの呼び出しも問題があります。

### AnimBPを作成する

AnimBPにて、VrmVMCノードを追加ください。

パラメータを2つセットします
 - VRM4U_VMC_Subsystemのデータ。受信した骨情報を参照します。
 - インポート時に生成されたMetaデータ。モデルのHumanoid骨名を参照します。

||
|-|
|[![](./assets/images/small/08a_node.png)](../assets/images/small/08a_node.png)|


### VMC Protocolを受け取る

`EUW_VMC` を起動します。
受信ポート番号を確認し、`RunServer` をクリックすれば完了です。

||
|-|
|[![](./assets/images/small/08a_panel.png)](../assets/images/small/08a_panel.png)|

正しく受信できた場合は、Widget上にログが表示されます。
全ての受信データを確認したい場合は、Widgetより `RawData` をOnにしてください。


Widgetにポート番号が表示されない場合は、OSCプラグインを有効化してください。
{: .notice--info}

----

## 応用編

### マップ上でプレビューする

`Animation in Editor` をONにしてください。エディタ上でそのままアニメーションが動作します。あくまでプレビュー動作です。正確にはPlayInで確認ください。

### ブレンドシェイプを受け取る

SubSystem内に受信した生データがあります。
`/VMC/Ext/Blend/Val:Blink` などで参照可能です。

### トラッカー情報を受け取る

`/VMC/Ext/Tra/Pos:LeftHand` などで参照可能です。

その他の受信データは、Widgetより `RawData` をOnにして確認ください。
