---
title: 「PWA Studio:Adobe Commerceに対する Venia GraphQL クエリで検証エラーが発生する」
description: この記事では、Venia ストアフロントのGraphQL クエリでAdobe Commerce インスタンスに対して検証エラーが発生する問題を解決する方法について推奨事項を説明します。
exl-id: ba268945-2a10-4af5-8089-cde21f0687bd
feature: GraphQL
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# PWA Studio:Adobe Commerceに対する Venia GraphQL クエリで検証エラーが発生する

この記事では、Venia ストアフロントのGraphQL クエリでAdobe Commerce インスタンスに対して検証エラーが発生する問題を解決する方法について推奨事項を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.2.x、2.3.x
* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x
* Adobe CommerceのPWA Studioプロジェクト

## 問題

Adobe Commerce オンプレミスまたはAdobe Commerce on cloud infrastructure への Venia GraphQL クエリが原因で検証エラーが発生する。

## 原因：

問題を引き起こす理由の 1 つは、Venia とそのGraphQL クエリが、接続されたAdobe Commerce インスタンスのスキーマと同期されていないことです。

## 解決策

クエリが最新かどうかをテストするには、プロジェクトルートで次のコマンドを実行します。

```bash
yarn run validate-queries
```

互換性レポートが表示されます。 互換性のない環境を使用している場合は、PWA StudioまたはAdobe Commerce インスタンスをアップグレードする必要があります。 [Adobe Commerce互換性マトリックス ](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/version-compatibility/) を確認して、必要なバージョンを確認してください。

アップグレード方法については、次のドキュメントを参照してください。

* PWA Studioのアップグレードの場合、アップグレードする必要があるバージョンを [PWAリリースノートの ](https://github.com/magento/pwa-studio/releases/) 以前のバージョンからのアップグレード」の節で検索します。
* 開発者向けドキュメントの [ クラウドインフラストラクチャー上のAdobe Commerceのバージョンのアップグレード ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version)
* [ 開発者向けドキュメントの ](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade)Adobe Commerceをオンプレミス（「composer create-project」またはアーカイブを使用してインストール）でアップグレードする
* [ 開発者向けドキュメントのAdobe Commerceをオンプレミスでアップグレード（Adobe Commerce リポジトリをクローンしてインストール） ](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/developer/git-installs)

## 関連資料

* [PWA Studio: コンパイルを開始する前に Webpack がハングします ](/help/troubleshooting/miscellaneous/pwa-studio-webpack-hangs-before-beginning-compilation.md) サポート サポート サポート サポート技術情報
* [PWA Studio：開発者モードの実行中に検証エラーが発生しました ](/help/troubleshooting/miscellaneous/pwa-studio-validation-errors-when-running-developer-mode.md) サポート技術情報
* [PWA Studio: サポート サポート サポート サポート技術情報で、ブラウザーに「Cannot proxy to」 ](/help/troubleshooting/miscellaneous/pwa-studio-browser-displays-cannot-proxy-to-error.md) エラーが表示される
* [PWA Studioを使用できるように NPM を設定 ](/help/how-to/general/configure-npm-to-be-able-to-use-pwa-studio.md) する（サポートナレッジベースを参照）
* [Adobe Commerce ドキュメントのPWA](https://magento.github.io/pwa-studio/)
