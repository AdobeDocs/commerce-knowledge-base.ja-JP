---
title: 'ACSD-53658: **[!UICONTROL Recently Viewed Product]ストア表示の** データが正しく更新されていません'
description: '**のAdobe Commerceの問題を修正するために、ACSD-53658 パッチを適用します。[!UICONTROL Recently Viewed Product]ストアビュー**データが正しく更新されない。'
feature: CMS, Personalization
role: Admin, Developer
exl-id: 4086dcee-37e5-4393-9048-ce19a2d248e9
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# ACSD-53658: **[!UICONTROL Recently Viewed Product]** ストア表示のデータが正しく更新されていません

ACSD-53658 パッチは、次の問題を修正します。 **[!UICONTROL Recently Viewed Product]** データがストア表示で正しく更新されない。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.42 がインストールされています。 パッチ ID は ACSD-53658 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この **[!UICONTROL Recently Viewed Product]** データがストア表示で正しく更新されない。

<u>再現手順</u>:

1. 管理パネルにログインします。
1. デフォルトの web サイトに対して 2 つ目のストア表示を作成します。
1. シンプルな製品を作成します。
1. 新しいストア表示に別の製品名を設定してください。
1. を作成 **[!UICONTROL Recently Viewed Product]** ウィジェット。
1. このウィジェットをホームページに表示するように設定します。
1. デフォルトストア表示からストアフロントの製品ページを開きます。
1. ホームページを開きます。
1. ストアスイッチャーを使用して、2 番目のストア表示に切り替えます。

<u>期待される結果</u>:

製品名がウィジェットに更新されます。

<u>実際の結果</u>:

ウィジェットの製品名は更新されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
