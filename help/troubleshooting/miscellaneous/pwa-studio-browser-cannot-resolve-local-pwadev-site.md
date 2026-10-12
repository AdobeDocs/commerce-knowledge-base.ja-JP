---
title: PWA Studio:.local.pwadev サイトを解決できません
description: この記事では、別のプログラムまたはプロセスが[ ホストファイル ] （https://en.wikipedia.org/wiki/Hosts_(file\）を編集し、プロジェクトドメインのエントリを削除した場合の解決策を紹介します。
exl-id: a1606016-906a-433f-9e40-9faa5f9bd790
feature: Configuration
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%
---
# PWA Studio:.local.pwadev サイトを解決できません

この記事では、別のプログラムまたはプロセスが[ ホストファイル ] （https://en.wikipedia.org/wiki/Hosts_(file\）を編集し、プロジェクトドメインのエントリを削除した場合の解決策を紹介します。

## 影響を受ける製品とバージョン

PWA Studio for Adobe Commerce

## イシュー

開発/ステージング サイトを参照すると、`.local.pwadev` サイトが表示されません。

## 原因

PWA Studioでは、プロジェクトのカスタムホスト名とSSL証明書をローカルコンピューターに割り当てることができます。 これには、コンピューターのホストファイルに、`my-storefront-project-abc123.local.pwadev`のように見える新しいエントリを作成することが含まれます。

このエントリは、開発者のコンピューター上のブラウザーに対して、そのURLにアクセスしたときにローカルのストアフロントプロジェクトを確認するように指示します。 別のプログラムまたはプロセスが入ってきて、そのエントリを削除した場合、ブラウザーはどこに行くかわからず、ブラウザーは`.local.pwadev` サイトを解決できません。

## Solution

[手動でホストファイル &#x200B;](https://docs.rackspace.com/docs/modify-your-hosts-file)を編集してエントリを再度追加できますが、他のインストール済みソフトウェアを調べて、以前の変更が上書きされたものを確認する必要があります。

## サポートナレッジベースの関連情報

* [PWA Studio：自己署名証明書の信頼エラー](https://support.magento.com/hc/en-us/articles/360038973172)
* [PWA Studio：コンパイルを開始する前にWebpackがハングする](/help/troubleshooting/miscellaneous/pwa-studio-webpack-hangs-before-beginning-compilation.md)
* [PWA Studio：ブラウザーに「次にプロキシできません」というエラーが表示される](/help/troubleshooting/miscellaneous/pwa-studio-browser-displays-cannot-proxy-to-error.md)
* [PWA Studio：開発者向けモードの実行時に検証エラーが発生する](/help/troubleshooting/miscellaneous/pwa-studio-validation-errors-when-running-developer-mode.md)
