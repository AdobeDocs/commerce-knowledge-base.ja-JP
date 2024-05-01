---
title: 「ACSD-48044：複数のギフトカードを適用すると、注文できなくなる」
description: 複数のギフト券を 1 件の注文に複数配送すると、注文ができなくなるAdobe Commerceの問題を修正するために、ACSD-48044 パッチを適用してください。
exl-id: fe57063c-d69c-4b80-a59c-912c2603f6af
feature: Admin Workspace, Gift, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# ACSD-48044：複数のギフトカードを適用すると、注文できなくなる

ACSD-48044 パッチは、複数のギフト カードを 1 つの注文に複数配送すると、注文できなくなる問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされています。 パッチ ID は ACSD-48044 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 - 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数のギフト カードを複数配送で 1 回の注文に適用すると、注文が行われなくなります。

<u>再現手順</u>:

1. クリーンなバージョンのAdobe Commerceをインストールします。
1. 価格が 100 ドルのシンプルな製品と、価格が 10 ドルの別のシンプルな製品を作成します。
1. にログインします [!UICONTROL Admin panel] そして、2 つのギフトカードを作成します。

   * 02KB8M0H0GRD = $50
   * 00GXM6SUGBLW = 25 ドル

1. 2 つのアドレスで顧客を作成します。
1. 2 つの製品を買い物かごに追加します。

   * 最初に 10 ドルの商品を追加し、次に 100 ドルの商品を追加します。 最初に$100 の商品を追加した場合、問題を再現できません。

1. 買い物かごに移動し、作成した 2 つのギフトカードを追加します。
1. クリックする **[!UICONTROL Ship to Multiple Addresses]** 買い物かごページに移動します。
1. 各製品を異なるアドレスに割り当てます。
1. に移動します **[!UICONTROL Shipping information]** ページ。
1. に移動します **[!UICONTROL Billing information]** ページ。
1. に移動します **[!UICONTROL Review Your Order]** ページで問題を確認できます。
1. 注文してみてください。

<u>期待される結果</u>:

* ギフトカードは合計金額に正しく適用されます。
* 注文が行われます。

<u>実際の結果</u>:

ギフトカードの金額がエラーと混在しています *「ギフトカードのコードを訂正してください。」* ご注文の際。

* 最初の製品：

   * ギフトカードの取り外し（00GXM6SUGBLW） - 15.00 ドル
   * ギフト カードを取り出す（02KB8M0H0GRD） - 0.00 ドル

* 2 番目の製品：

   * ギフトカードの取り外し（00GXM6SUGBLW） - 25.00 ドル
   * ギフト カードを取り出す（02KB8M0H0GRD） - 35.00 ドル

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
