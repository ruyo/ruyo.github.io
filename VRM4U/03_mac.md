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
慣れ次第で、数分～1時間くらいでセットアップ完了します。気軽にお試しください。

ソースの取得とプロジェクトビルドを行います。エンジンビルドは不要です。

### 手順の要約

 - カスタム版assimpをダウンロード、makeする。
 - VRM4Uのソースをダウンロード、展開する
   - assimpのdylibをThirdParty以下にコピー
 - MyProject.uprojectを右クリック、Xcodeプロジェクトを作成しビルド。

ソースの取得方法や展開場所は[こちらのページを参照ください。](../03_exe/)

私はMacの開発環境に不慣れです。詳しい方はより適した手順で導入ください…
{: .notice--info}

### assimpのビルド

こちらからカスタム版assimpのソースをダウンロード、makeします。

https://github.com/ruyo/assimp

私は`cmake-gui`を利用しました。guiでパスを設定後、`Configure`、`Generate` を押します。途中で出るダイアログはデフォルトままでOKです。

オプションが多数ありますが、そのままで構いません。（できれば`ASSIMP_INSTALL`はOFFが良いと思います）

||
|-|
|[![](./assets/images/small/03m_c1.png)](../assets/images/03m_c1.png)|

続いてターミナルより、assimpディレクトリで、`make` コマンドを実行します。

完了すると、binディレクトリ（上の例だとassimp/build2/bin）に`libassimp.dylib` が生成されます。

### プロジェクトのビルド

UE4からC++プロジェクトを作成しておきます。
VRM4Uのソースをプロジェクトに展開し、前段でmakeしたassimpライブラリを以下に置きます。

MyProject/Plugins/VRM4U/ThirdParty/assimp/lib/Mac/libassimp.dylib


その後、MyProject.uprojectをダブルクリック、ダイアログでYesを選択し、ビルドします。

|ダイアログの Yes でプロジェクトがビルドされます|
|-|
|[![](./assets/images/small/03m_c3.png)](../assets/images/03m_c3.png)|

起動した場合は次の手順へ進んでください。

途中でエラーが出る場合は、Xcodeからビルドします。.uprojectファイルを右クリック、Xcodeプロジェクトを作成します。.xcworkspaceが生成されるので開きます。

||
|-|
|[![](./assets/images/small/03m_c2.png)](../assets/images/03m_c2.png)|

Xcodeでビルド。Product > Build を選択します。完了後はMyProject.uprojectをダブルクリックで起動します。

||
|-|
|[![](./assets/images/small/03m_c4.png)](../assets/images/03m_c4.png)|

初回起動時はプラグインは無効です。プラグイン設定から有効化してください。有効化後、再度Xcodeでビルドしてください。

||
|-|
|[![](./assets/images/small/03m_c5.png)](../assets/images/03m_c5.png)|


完了です。

|Mac上でのモデルインポート||
|-|-|
|[![](./assets/images/small/03m_i1.png)](../assets/images/03m_i1.png)|[![](./assets/images/small/03m_i2.png)](../assets/images/03m_i2.png)|

蛇足：もしiOSアプリを作成したい場合、Windowsからのリモートビルドも利用することができます。用途に応じて環境をご利用ください。
{: .notice--info}
