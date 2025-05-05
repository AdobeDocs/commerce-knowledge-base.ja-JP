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

# ACSD-47908:*0 以下の値が想定されます* チェックアウト中にエラーが発生しました

チェックアウト時の出荷手順でソースと数量を選択する際に、ACSD-47908 パッチによってエラー *0 以下の値が想定される* が修正されます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされている場合に使用できます。 パッチ ID は ACSD-47908 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

チェックアウト中に出荷ステップでソースと数量を選択すると、次のエラーがスローされます。*0 以下の値が想定されます*。

<u> 前提条件 </u>:

Adobe Commerce Inventory management（MSI）モジュールをインストールします。

<u> 再現手順 </u>:

1. **[!UICONTROL Stores]**/**[!UICONTROL Inventory]**/**[!UICONTROL Sources]** に移動し、複数のソースを設定します。
1. **[!UICONTROL Stores]**/**[!UICONTROL Inventory]**/**[!UICONTROL Stock]** に移動し、新しい在庫を作成します。
   * 次に、ソースを新しい在庫に割り当てます。
1. **[!UICONTROL Catalog]**/**[!UICONTROL Products]** に移動し、少なくとも 1 つの製品を編集します。
   * 製品が新しいソースに割り当てられていることを確認し、使用可能な数量を指定します。
1. **[!UICONTROL Sales]**/**[!UICONTROL Orders]** に移動し、新しい注文を作成します。
1. その商品を注文に追加して配置します。
1. 「**[!UICONTROL Ship]**」をクリックします。
1. 出荷元のソースを選択します。
1. 出荷する各品目の数量を指定します。
1. ページをリロードします。
1. 「**[!UICONTROL Proceed to Shipment]**」をクリックします。

<u> 期待される結果 </u>:

新しい出荷ページがエラーなしで開きます。

<u> 実際の結果 </u>:

* 入力した数量は検証できません。
* 次のエラーがスローされます。*0 以下の値を入力してください*。

  ただし、このエラーは一貫性がなく、常に表示されるとは限りません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
