---
title: 「ACSD-48300：設定可能な製品が削除された場合、返しを作成できない」
description: 設定可能な商品が削除されると返品を作成できないAdobe Commerceの問題を修正するために、ACSD-48300 パッチを適用してください。
exl-id: 4abbc398-b341-4ff6-9483-9cf8f3dbbfbb
feature: Admin Workspace, Configuration, Orders, Products, Returns
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# ACSD-48300：設定可能な製品が削除されている場合、返品を作成できない

ACSD-48300 パッチは、設定可能な製品が削除された場合にリターンを作成できない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされています。 パッチ ID は ACSD-48300 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な商品が削除されている場合、返品を作成することはできません。

<u>再現手順</u>:

1. ストアフロントの RMA を有効にする場所 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Sales]** > **[!UICONTROL RMA Settings]**.
1. 設定可能な商品を作成します。
1. ストアフロントで、アカウントを作成（またはログイン）します。
1. 設定可能な製品を最初の項目として買い物かごに追加します。
1. 後で簡単な製品を追加してください。
1. 注文します。
1. 注文を発送します。
1. ここで、設定可能な製品のみを削除します（子製品は削除しないでください）。
1. ストアフロントで、に移動します **[!UICONTROL My Orders]** オーダーを表示します。
1. クリックする **[!UICONTROL Return]**.

<u>期待される結果</u>:

管理者は、設定可能な商品が削除された場合でも、項目を返すことができます。

<u>実際の結果</u>:

項目を返す際にエラーが発生します。

```
report.CRITICAL: Error: Call to a member function getShipmentType() on null in magento2ee/app/code/Magento/Rma/view/frontend/templates/return/create.phtml:52
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
