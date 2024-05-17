---
title: 「ACSD 49843：で自動請求されると、製品ダウンロードリンクを使用できなくなります [!UICONTROL Payment Action] = [!UICONTROL Intent Sale]'
description: 注文した商品がオンライン支払い方法によって自動請求された後、商品のダウンロードリンクが利用できなくなるAdobe Commerceの問題を修正するために、ACSD-49843 パッチを適用してください。 [!UICONTROL Payment Action] はに設定されています。 [!UICONTROL Intent Sale].
feature: Catalog Management, Configuration, Invoices, Orders, Storefront
role: Admin, Developer
exl-id: 4bfa3827-a2b1-4168-a39c-99c617ee4795
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# ACSD-49843：で自動請求後、製品のダウンロードリンクを使用できない [!UICONTROL Payment Action] = [!UICONTROL Intent Sale]

ACSD-49843 パッチは、次の場合にオンライン支払い方法によって注文された商品が自動請求された後、製品のダウンロードリンクが使用できなくなる問題を修正しました [!UICONTROL Payment Action] はに設定されています。 [!UICONTROL Intent Sale]. このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.37 がインストールされています。 パッチ ID は ACSD-49843 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.3.7-p4、2.4.1 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

オンライン支払い方法で注文品目を自動請求すると、製品のダウンロードリンクは次の場合に使用できません [!UICONTROL Payment Action] はに設定されています。 [!UICONTROL Intent Sale].

<u>再現手順</u>:

1. Adobe Commerce Admin にログインし、に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Configure Braintree]**.

   * が含まれる [!UICONTROL Payment Action] ドロップダウンで次を選択 **[!UICONTROL Intent Sale]**、およびを設定 *[!UICONTROL Enable Card Payments]* 対象： *はい*.

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Downloadable Product Option]** > **[!UICONTROL Order Item status for Download]**。に設定されていることを確認します。 *「請求済み」*.
1. ストアフロントで、顧客としてログインします。

   * ダウンロード可能な製品とシンプルな製品を買い物かごに追加します。
   * 使用方法 [!DNL Braintree Pay] カード オプションを使用して注文する。

1. に移動 **[!UICONTROL My Orders]** 注文の請求書が自動的に作成され、両方の品目ステータスが次のようになっていることを確認します *「請求済み」*.
1. に移動 **[!UICONTROL My Downloadable Products]** ダウンロードリンクがまだ使用できないことを確認します。
1. 管理者で、その注文に移動し、その注文の出荷を作成します。
1. ストアフロントで、に移動します **[!UICONTROL My Downloadable Products]** ダウンロードリンクが使用可能になったことを確認します。

<u>期待される結果</u>:

ダウンロードリンクは、ダウンロード可能な製品ステータスが「」の場合に使用できます。 *「請求済み」*.

<u>実際の結果</u>:

ダウンロード可能な製品ステータスに「」と表示されている場合でも、ダウンロードリンクは使用できません。 *「請求済み」*. 物理的な製品の出荷が作成された後にのみ使用できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
