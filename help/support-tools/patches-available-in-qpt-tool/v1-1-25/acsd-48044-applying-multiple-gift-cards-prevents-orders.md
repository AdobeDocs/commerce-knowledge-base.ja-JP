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

ACSD-48044 パッチは、複数のギフト カードを 1 つの注文に複数配送すると、注文できなくなる問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされている場合に使用できます。 パッチ ID は ACSD-48044 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 - 2.4.5-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数のギフト カードを複数配送で 1 回の注文に適用すると、注文が行われなくなります。

<u> 再現手順 </u>:

1. クリーンなバージョンのAdobe Commerceをインストールします。
1. 価格が 100 ドルのシンプルな製品と、価格が 10 ドルの別のシンプルな製品を作成します。
1. [!UICONTROL Admin panel] にログインし、2 つのギフトカードを作成します。

   * 02KB8M0H0GRD = $50
   * 00GXM6SUGBLW = 25 ドル

1. 2 つのアドレスで顧客を作成します。
1. 2 つの製品を買い物かごに追加します。

   * 最初に 10 ドルの商品を追加し、次に 100 ドルの商品を追加します。 最初に$100 の商品を追加した場合、問題を再現できません。

1. 買い物かごに移動し、作成した 2 つのギフトカードを追加します。
1. 買い物かごページで「**[!UICONTROL Ship to Multiple Addresses]**」をクリックします。
1. 各製品を異なるアドレスに割り当てます。
1. **[!UICONTROL Shipping information]** のページに移動します。
1. **[!UICONTROL Billing information]** のページに移動します。
1. **[!UICONTROL Review Your Order]** ページに移動すると、イシューを確認できます。
1. 注文してみてください。

<u> 期待される結果 </u>:

* ギフトカードは合計金額に正しく適用されます。
* 注文が行われます。

<u> 実際の結果 </u>:

「ギフトカードのコードを修正してください *というエラーがギフトカードの金額に含まれています。注文する際に* します。

* 最初の製品：

   * ギフトカードの取り外し（00GXM6SUGBLW） - 15.00 ドル
   * ギフト カードを取り出す（02KB8M0H0GRD） - 0.00 ドル

* 2 番目の製品：

   * ギフトカードの取り外し（00GXM6SUGBLW） - 25.00 ドル
   * ギフト カードを取り出す（02KB8M0H0GRD） - 35.00 ドル

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
