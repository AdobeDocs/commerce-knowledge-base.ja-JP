---
title: 「ACSD-50116：管理者ユーザーは、レベル 3 以下のサブカテゴリの URL 書き換えを作成できません」
description: ACSD-50116 パッチを適用すると、管理者ユーザーがレベル 3 以下のサブカテゴリの URL 書き換えを作成できないAdobe Commerceの問題を修正できます。
exl-id: 3fa8ebc1-b55d-437e-9dc7-bf6c300b9bbe
feature: Admin Workspace, Categories
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# ACSD-50116：管理者ユーザーは、レベル 3 以下のサブカテゴリの URL 書き換えを作成できません

ACSD-50116 パッチを使用すると、管理者ユーザーがレベル 3 以下のサブカテゴリの URL 書き換えを作成できない問題を修正できます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は ACSD-50116 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーは、レベル 3 以下のサブカテゴリに対して URL の書き換えを作成することはできません。

<u>再現手順</u>:

1. 3 つ以上のレベルのサブカテゴリを含むカテゴリ ツリーを作成します。
1. を作成してみてください *[!UICONTROL URL Rewrite]* レベル 4 のカテゴリで両方を使用する *[!UICONTROL For Product]* および *[!UICONTROL For Category]* オプション。

<u>期待される結果</u>:

カテゴリ ツリーには、レベル 4 以下のサブカテゴリが表示されます。

<u>実際の結果</u>:

カテゴリ ツリーには、レベル 3 までのサブカテゴリのみが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
