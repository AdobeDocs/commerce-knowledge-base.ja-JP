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

この記事では、「」というメッセージが表示された場合の解決策を説明します&#x200B;*プラグイン VCL のバージョンが古くなっています。 再アップロードしてください。*&#x200B;最新の Fastly モジュールをインストールしていないことが原因で、Commerce Admin の Fastly Configuration に「」が表示されます。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce 2.2.x.、2.3.x<br>
Fastly：このエラーは、最新のバージョンを除く、Fastly モジュールのすべてのバージョンに影響を与える可能性があります。 最新のリリースについて詳しくは、を参照してください。 [Fastly リリースノート](https://github.com/fastly/fastly-magento2/releases) GitHub で。

## 問題

1. Commerce管理パネルにログインします。
1. に移動します。 **ストア** > **設定** > **詳細** > **システム** > **フルページキャッシュ**   **Fastly キャッシュ。**
1. が含まれる **自動アップロードおよびサービスアクティベーション** セクションには、「*プラグイン VCL のバージョンが古くなっています。 再アップロードしてください。*」通知。
1. 「Upload VCL to Fastly」ボタンをクリックして VCL スニペットをアップロードしようとしますが、まだ警告が表示されます。*プラグイン VCL のバージョンが古くなっています。 再アップロードしてください。*“

## 原因：

Fastly 拡張機能は（バンドルされた VCL 設定およびテンプレートと共に）更新されましたが、更新された VCL 設定は Fastly サービスにアップロードされていません。 Adobe Commerce モジュールを更新する場合 `Fastly_Cdn`の場合は、更新した VCL 設定を Fastly に再度アップロードする必要があります。

## 解決策

1. 最新の ECE ツールがインストールされていること、およびで確認します。 [現在のバージョン](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/release-notes/cloud-tools-suite.html) 開発者向けドキュメントを参照してください。 ECE-Tools には、依存関係に Fastly パッケージのバージョンがあります。

   これは Fastly プラグインの最新バージョンではない可能性がありますが、現在インストールされているものより新しいバージョンである可能性が高く、最新の ECE-Tools をインストールすることをお勧めします。

1. 現在のバージョンの ECE-Tools を使用していない場合は、次の手順に従って操作します [アップグレード](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package.html) 開発者向けドキュメントを参照してください。
1. ECE-Tools をアップグレードしたら、の最新バージョンがあるかどうかを確認します。 [Fastly プラグイン](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets) インストールされています。
1. Fastly プラグインが現在のバージョンでない場合は、次の手順に従って操作します。 [プラグインの最新バージョンへのアップグレード](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#upgrade-the-fastly-module) 開発者向けドキュメントを参照してください。

## 関連資料

* Fastly の設定について詳しくは、以下を参照してください。 [Fastly サービスの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/fastly.html) 開発者向けドキュメントを参照してください。
* Fastly の一般的な情報については、を参照してください [fastly.com](https://www.fastly.com/).
