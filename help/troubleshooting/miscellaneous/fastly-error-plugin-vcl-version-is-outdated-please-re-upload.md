---
title: 「Fastly エラー：プラグイン VCL バージョンが古くなっています。 Please re-Upload'
description: この記事では、「*プラグイン VCL バージョンが古くなっています！ 再アップロードしてください。最新の Fastly モジュールをインストールしていないことが原因で、Commerce Admin の Fastly Configuration に*"。
exl-id: d7870e9e-ba6b-49c2-a80c-26fb464cbae3
feature: Best Practices, Cache
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Fastly エラー：プラグイン VCL のバージョンが古くなっています。 再アップロードしてください

この記事では、「*プラグイン VCL バージョンが古くなっています！ 再アップロードしてください。最新の Fastly モジュールをインストールしていないことが原因で、Commerce Admin の Fastly Configuration に「*」が表示されます。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce 2.2.x.、2.3.x<br>
Fastly：このエラーは、最新のバージョンを除く、Fastly モジュールのすべてのバージョンに影響を与える可能性があります。 最新リリースについて詳しくは、GitHub の [Fastly リリースノート ](https://github.com/fastly/fastly-magento2/releases) を参照してください。

## 問題

1. Commerce管理パネルにログインします。
1. **ストア**/**設定**/**詳細**/**システム**/**フルページキャッシュ** に移動します   **Fastly キャッシュ。**
1. 「**自動アップロードとサービスアクティベーション**」セクションには、「*プラグイン VCL バージョンが古くなっています！ 再アップロードしてください。*」通知です。
1. 「Upload VCL to Fastly」ボタンをクリックして VCL スニペットをアップロードしようとしても、「*プラグイン VCL バージョンが古くなっています！ もう一度アップロードしてください。*」

## 原因：

Fastly 拡張機能は（バンドルされた VCL 設定およびテンプレートと共に）更新されましたが、更新された VCL 設定は Fastly サービスにアップロードされていません。 Adobe Commerce モジュール `Fastly_Cdn` を更新する場合は、更新された VCL 設定を Fastly に再度アップロードする必要があります。

## 解決策

1. 最新の ECE ツールがインストールされていること、および [ 現在のバージョン ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/release-notes/cloud-tools-suite.html?lang=ja) が開発者向けドキュメントに記載されていることを確認します。 ECE-Tools には、依存関係に Fastly パッケージのバージョンがあります。

   これは Fastly プラグインの最新バージョンではない可能性がありますが、現在インストールされているものより新しいバージョンである可能性が高く、最新の ECE-Tools をインストールすることをお勧めします。

1. 現在のバージョンの ECE-Tools を使用していない場合は、開発者向けドキュメントで次の手順に従って [ アップグレード ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package.html?lang=ja) してください。
1. ECE-Tools をアップグレードしたら、現在のバージョンの [Fastly プラグイン ](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets) がインストールされているかどうかを確認します。
1. Fastly プラグインが最新バージョンでない場合は、開発者向けドキュメントで次の手順に従って [ プラグインを最新バージョンにアップグレード ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html?lang=ja#upgrade-the-fastly-module) してください。

## 関連資料

* Fastly のセットアップと設定について詳しくは、開発者向けドキュメントの [Fastly サービスの設定 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/fastly.html?lang=ja) を参照してください。
* Fastly の一般的な情報については、[fastly.com](https://www.fastly.com/) を参照してください。
