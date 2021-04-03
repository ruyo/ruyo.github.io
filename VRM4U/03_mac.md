---
title: "MacでVRM4Uを利用する"
---


||
|-|
|[![](./assets/images/small/03m_i2.png)](../assets/images/03m_i2.png)|
|モデル：[千駄ヶ谷 渋](https://hub.vroid.com/characters/675572020956181239/models/4479743608263344465)|


----

## 概要

MacでVRM4Uを動かすための環境設定をします。
UE4が動作できるスペックがあれば数分で完了します。気軽に利用ください。

ソースの取得とプロジェクトビルドを行います。エンジンビルドは不要です。

### 手順の要約

 - VRM4Uのソースをダウンロード、展開する
 - カスタム版assimpをダウンロード、makeする。
   - dylibをThirdParty以下にコピー
 - MyProject.uprojectを右クリック、Xcodeプロジェクトを作成しビルド。

ソースの取得や展開場所は[こちらのページを参照ください。](../03_exe/)

私はMacの開発環境に不慣れです。詳しい方はより適した手順で導入ください…
{: .notice--info}

### assimpのビルド

こちらからカスタム版assimpのソースをダウンロード、makeします。

https://github.com/ruyo/assimp

私は`cmake-gui`を利用しました。参考にどうぞ。
オプションがよくわからない場合、そのままで構いません。（ただ`ASSIMP_INSTALL`はOFFが良いと思います）

パスを設定後、`Configure`、`Generate` を押します。途中で出るダイアログはデフォルトままでOKです。

||
|-|
|[![](./assets/images/small/03m_c1.png)](../assets/images/03m_c1.png)|

続いてターミナルより、assimpディレクトリで、`make` コマンドを実行します。

完了すると、binフォルダ（上の例だとassimp/build2/bin）に`libassimp.dylib` などが生成されます。

### プロジェクトのビルド

UE4からC++プロジェクトを作成しておきます。
VRM4Uのソースをプロジェクトに展開し、前段でmakeしたassimpライブラリを以下に置きます。リンクでも構いません。

MyProject/Plugins/VRM4U/ThirdParty/assimp/lib/Mac/libassimp.dylib


その後、MyProject.uprojectをダブルクリックしてビルド＆起動します。

|Yes でビルドされます|
|-|
|[![](./assets/images/small/03m_c3.png)](../assets/images/03m_c3.png)|

起動した場合は次の手順へ進んでください。

途中でエラーが出る場合は、Xcodeからビルドします。ファイルを右クリック、Xcodeプロジェクトを作成し開きます。

||
|-|
|[![](./assets/images/small/03m_c2.png)](../assets/images/03m_c2.png)|

Xcodeでビルドします。Product > Build を選択します。完了後はMyProject.uprojectをダブルクリックで起動します。

以下のページに軽く触れられています。

https://docs.unrealengine.com/en-US/ProductionPipelines/DevelopmentSetup/CompilingProjects/index.html


初回起動時はプラグインは無効です。プラグイン設定から有効化してください。[詳しくはこちら](../01_quick-start/)。有効化後、再度Xcodeでビルドしてください。

完了です。

|Mac上でのモデルインポート||
|-|-|
|[![](./assets/images/small/03m_i1.png)](../assets/images/03m_i1.png)|[![](./assets/images/small/03m_i2.png)](../assets/images/03m_i2.png)|

蛇足：もしiOSアプリを作成したい場合、Windowsからのリモートビルドも利用することができます。用途に応じて環境をご利用ください。
{: .notice--info}
