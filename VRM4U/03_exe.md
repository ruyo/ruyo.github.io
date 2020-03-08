---
title: "配布用EXEを作成する"
---

----

## EXE作成に必要なファイルをダウンロードする

GitHubアカウントとEpicGamesアカウントの紐付けが必要です。
{: .notice--info}

[こちらのリンク](https://github.com/ruyo/UnrealEngine_VRM4UPlugin)より、VRM4Uのソース入りzipをダウンロードします。

404エラーページが出る場合は紐付けが必要です。[こちらのリンク](https://www.unrealengine.com/ja/blog/updated-authentication-process-for-connecting-epic-github-accounts)よりGitHubアカウントの紐付けを行ってください。


||
|-|
|[![](./assets/images/small/03e_exe.png)](../assets/images/03e_exe.png)|

導入は従来のプラグイン同様 `MyProject/Plugins/VRM4U` となるよう配置すれば完了です。

----
## EXEを作る

VisualStudioによるビルド環境が必要です。セットアップ済であれば、UE4のメニューからパッケージ作成可能です。

## なんでこんなに面倒くさいの？

プラグインを作る際、一部エンジンのソースを参考にしているためです。主にランタイムロード機能です。

念の為にEpic紐付けのアカウントで公開しています。（もしかしたら問題ないかもしれません）

