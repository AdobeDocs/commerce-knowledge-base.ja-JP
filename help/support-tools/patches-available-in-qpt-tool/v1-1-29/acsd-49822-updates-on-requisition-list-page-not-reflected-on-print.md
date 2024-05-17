---
title: 「ACSD-49822：購買依頼リスト・ページの更新が印刷購買依頼リストに反映されない」
description: ACSD-49822 パッチを適用して、購買依頼リスト・ページの更新が印刷購買依頼リストに反映されないAdobe Commerceの問題を修正します。
exl-id: 584e3fcd-9153-41aa-8857-cf1fa41269c9
feature: Admin Workspace, B2B
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# ACSD-49822：購買依頼リストの更新が印刷購買依頼リストに反映されない

ACSD-49822 パッチにより、購買依頼リスト ページの更新が印刷購買依頼リストに反映されない問題が修正されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされています。 パッチ ID は ACSD-49822 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

購買依頼リスト・ページの更新は、印刷購買依頼リストには反映されません。

<u>再現手順</u>:

1. に移動して購買依頼リストを使用可能にします。 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[B2B の機能]**.
1. 商品を作成します。
1. 顧客としてログインし、2 つの製品を購買依頼リストに追加します。
1. に移動 **[!UICONTROL My Account]** > **[!UICONTROL My Requisition Lists]**.
1. 購買依頼リストの表示
1. クリック **[!UICONTROL Print]** 右上隅
1. 「印刷」ウィンドウを閉じて、購買依頼リスト・ページを印刷します。
1. リストのアイテムを削除するか、アイテムの数量を更新してから、もう一度印刷してみてください。
1. 項目が印刷ウィンドウで更新されていないことがわかります。
1. 印刷ウィンドウを閉じます。
1. 品目が購買依頼リスト印刷ページで更新されていないことを確認します。

<u>期待される結果</u>:

印刷するリストは、変更が適用された後に更新されます。

<u>実際の結果</u>:

更新は、購買依頼リスト印刷ページには反映されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
