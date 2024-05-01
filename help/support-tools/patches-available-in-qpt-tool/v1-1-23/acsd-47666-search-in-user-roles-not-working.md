---
title: 'ACSD-47666：での検索 [!UICONTROL User Roles] 動作しない'
description: ACSD-47666 パッチを適用して、フィルターが機能するAdobe Commerceの問題を修正してください [!UICONTROL User Roles] が期待どおりに動作しない。
exl-id: c1b6d3ab-e132-4b09-8692-2b82f9ca6864
feature: Roles/Permissions, Search
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# ACSD-47666：での検索 **[!UICONTROL User Roles]** 動作しない

ACSD-47666 パッチは、での検索の問題を解決します。 **[!UICONTROL User Roles]** は動作していません。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.23 がインストールされています。 パッチ ID は ACSD-47666 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

フィルター関数： **[!UICONTROL User Roles]** が期待どおりに動作しない。

<u>再現手順</u>:

1. Adobe Commerce管理者にログインします。 **[!UICONTROL System]** > **[!UICONTROL Permissions]** > **[!UICONTROL User Roles]**.
1. リストから既存の役割を開きます。
1. を開きます **[!UICONTROL Role Users]** タブ。
1. 列にクエリを入力します。
1. Enter キーを押します。

<u>期待される結果</u>:

この **[!UICONTROL User Roles]** filter 関数は、クエリに基づいて結果をフィルタリングする必要があります。

<u>実際の結果</u>:

コンソールエラーを伴う無限読み込み _（インデックス）:9 キャッチされない TypeError: NULL のプロパティを読み取れません（&#39;down&#39;を読み取ります）_.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。 

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
