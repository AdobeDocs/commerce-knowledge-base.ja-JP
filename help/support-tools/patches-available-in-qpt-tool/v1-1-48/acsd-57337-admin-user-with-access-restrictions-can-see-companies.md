---
title: 「ACSD-57337：アクセス制限を持つ管理者ユーザーが、*会社* グリッドのすべての会社を表示できる」
description: ACSD-57337 パッチを適用すると、特定の web サイトへのアクセス制限を持つ管理者ユーザーが*会社* グリッドのすべての web サイトの会社を表示できるAdobe Commerceの問題を修正できます。
feature: Companies, B2B, Configuration
role: Admin, Developer
source-git-commit: a02c80006f1c8a434fe17322f0c6cee25f086396
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# ACSD-57337：アクセス制限を持つ管理者ユーザーが、 *会社* グリッド

ACSD-57337 パッチは、特定の web サイトへのアクセス制限を持つ管理者ユーザーが、内のすべての web サイトの会社を表示できる問題を修正します *会社* グリッド。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされています。 パッチ ID は ACSD-57337 です。 この問題はAdobe Commerce 2.5.0 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

特定の web サイトへのアクセス制限を持つ管理者ユーザーは、内のすべての web サイトの会社を表示できます。 *会社* グリッド。

<u>再現手順</u>:

1. 追加の web サイトを作成し、保存およびレビューします。
1. 異なる web サイトに割り当てられている会社をいくつか作成します。
1. 管理者ユーザーロールを作成し、作成した web サイトにロール範囲を設定します。
1. 管理者を作成し、作成した役割に割り当てます。
1. 新しい管理者でログインします。
1. 開く **[!UICONTROL Customers]** > **[!UICONTROL Companies]** 会社のリストを確認します。

<u>期待される結果</u>:

追加の web サイトに割り当てられている会社は、 *会社* グリッド。

<u>実際の結果</u>:

すべての会社が「」に表示される *会社* グリッド。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。