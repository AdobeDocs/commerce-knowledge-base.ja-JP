---
title: 「ACSD-47908:*0 以下の値が必要です* チェックアウト中にエラーが発生しました」
description: チェックアウト時に発送手順でソースと数量を選択する際に、Adobe Commerceエラー*0 以下の値が想定されます*を修正するために ACSD-47908 パッチを適用してください。
exl-id: fec90e4b-9cb8-4cd9-9e85-ccada840c896
feature: Admin Workspace, Checkout, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# ACSD-47908: *0 以下の値を指定してください* チェックアウト中のエラー

ACSD-47908 パッチによってエラーが修正されます *0 以下の値を指定してください* チェックアウト時の出荷手順でソースと数量を選択する場合。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされています。 パッチ ID は ACSD-47908 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

チェックアウト中の出荷手順でソースと数量を選択すると、次のエラーがスローされる。 *0 以下の値を指定してください*.

<u>前提条件</u>:

Adobe Commerce Inventory management（MSI）モジュールをインストールします。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Inventory]** > **[!UICONTROL Sources]** 複数のソースを設定します。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Inventory]** > **[!UICONTROL Stock]** 新しい在庫を作成します。
   * 次に、ソースを新しい在庫に割り当てます。
1. に移動 **[!UICONTROL Catalog]** > **[!UICONTROL Products]** を選択し、1 つ以上の製品を編集します。
   * 製品が新しいソースに割り当てられていることを確認し、使用可能な数量を指定します。
1. に移動 **[!UICONTROL Sales]** > **[!UICONTROL Orders]** 新しい注文を作成します。
1. その商品を注文に追加して配置します。
1. クリック **[!UICONTROL Ship]**.
1. 出荷元のソースを選択します。
1. 出荷する各品目の数量を指定します。
1. ページをリロードします。
1. クリックする **[!UICONTROL Proceed to Shipment]**.

<u>期待される結果</u>:

新しい出荷ページがエラーなしで開きます。

<u>実際の結果</u>:

* 入力した数量は検証できません。
* 次のエラーが発生します。 *0 以下の値を入力してください*.

  ただし、このエラーは一貫性がなく、常に表示されるとは限りません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
