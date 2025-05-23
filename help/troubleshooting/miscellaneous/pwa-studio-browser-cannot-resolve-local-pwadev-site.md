---
title: 「PWA Studio：ブラウザーが.local.pwadev サイトを解決できない」
description: この記事では、別のプログラムまたはプロセスが [ ホスト ファイル ] （https://en.wikipedia.org/wiki/Hosts_(file）を編集し、プロジェクト ドメインのエントリを削除した場合の解決策を示します。
exl-id: a1606016-906a-433f-9e40-9faa5f9bd790
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# PWA Studio: ブラウザーが.local.pwadev サイトを解決できません

この記事では、別のプログラムまたはプロセスが自分の [ ホスト ファイル ] （https://en.wikipedia.org/wiki/Hosts_(file\））を編集し、自分のプロジェクト ドメインのエントリを削除した場合の解決策を示します。

## 影響を受ける製品とバージョン

Adobe CommerceのPWA Studio

## 問題

開発/ステージングサイトを参照しても、`.local.pwadev` サイトは表示されません。

## 原因：

PWA Studioを使用すると、プロジェクトのカスタム ホスト名と SSL 証明書をローカルコンピューターに割り当てることができます。 これには、コンピューターのホストファイルに、`my-storefront-project-abc123.local.pwadev` のような新しいエントリを作成することが含まれます。

このエントリは、開発者のコンピューター上のすべてのブラウザーに、その URL にアクセスしたときにローカルストアフロントプロジェクトを参照するように指示します。 別のプログラムまたはプロセスが入ってきて、そのエントリを削除すると、ブラウザーは移動先を認識できず、ブラウザーは `.local.pwadev` サイトを解決できません。

## 解決策

[ ホストファイルを手動で編集 ](https://support.rackspace.com/how-to/modify-your-hosts-file/) してエントリを追加し直すこともできますが、インストールされている他のソフトウェアを調べて、以前の変更を上書きしたものを確認する必要があります。

## サポートナレッジベースの関連資料

* [PWA Studio：自己署名証明書の信頼エラー ](https://support.magento.com/hc/en-us/articles/360038973172)
* [PWA Studio: コンパイルを開始する前に webpack がハングします](/help/troubleshooting/miscellaneous/pwa-studio-webpack-hangs-before-beginning-compilation.md)
* [PWA Studio：ブラウザーに「Cannot proxy to」エラーが表示される](/help/troubleshooting/miscellaneous/pwa-studio-browser-displays-cannot-proxy-to-error.md)
* [PWA Studio：開発者モードの実行中に検証エラーが発生する](/help/troubleshooting/miscellaneous/pwa-studio-validation-errors-when-running-developer-mode.md)
