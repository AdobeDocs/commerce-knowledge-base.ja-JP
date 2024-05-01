---
title: 「MDVA-43859：削除された顧客がログインしたときに、「customerId =を持つそのようなエンティティがありません」というエラーが記録される」
description: MDVA-43859 パッチでは、削除されたお客様がログインしようとすると、エラー*No such entity with customerId =*がログに記録される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.14 がインストールされている場合に利用できます。 パッチ ID は MDVA-43859。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 62c4b6ee-88a0-40b8-9eb2-37b6cefa0b83
feature: Variables
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# MDVA-43859：削除された顧客がログインしたときに、「No such entity with customerId =」というエラーが記録される

MDVA-43859 パッチを適用すると、エラーが発生する問題が修正されます *customerId =の該当するエンティティがありません* 削除された顧客がログインしようとすると、がログに記録されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.14 がインストールされています。 パッチ ID は MDVA-43859。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

エラー *customerId =の該当するエンティティがありません* 削除された顧客がログインしようとすると、がログに記録されます。

<u>再現手順</u>:

1. フロントエンドから顧客アカウントを作成します。
1. 手順 1 で作成した顧客アカウントからログアウトしてログインします。
1. 別のブラウザーでバックエンドを読み込み、カスタマーグリッドに移動します。
1. 手順 1 で作成した顧客を削除します。
1. 最初のブラウザーに戻り、ログアウトしてみてください。

<u>期待される結果</u>:

ユーザーはエラーなくログインページにリダイレクトされます。

<u>実際の結果</u>:

お客様に次のエラーが表示される。 *customerId =の該当するエンティティがありません*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
