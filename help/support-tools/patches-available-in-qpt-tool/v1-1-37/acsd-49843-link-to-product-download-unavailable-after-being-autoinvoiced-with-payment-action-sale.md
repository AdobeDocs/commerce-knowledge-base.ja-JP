---
title: 「ACSD 49843:[!UICONTROL Payment Action] = [!UICONTROL Intent Sale] で自動請求後、製品ダウンロードリンクを使用できません」
description: ACSD-49843 パッチを適用すると、[!UICONTROL Payment Action] が [!UICONTROL Intent Sale] に設定されている場合に、オンライン支払い方法によって注文された商品が自動請求された後に商品のダウンロードリンクが使用できなくなるAdobe Commerceの問題を修正できます。
feature: Catalog Management, Configuration, Invoices, Orders, Storefront
role: Admin, Developer
exl-id: 4bfa3827-a2b1-4168-a39c-99c617ee4795
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# ACSD-49843:[!UICONTROL Payment Action] = [!UICONTROL Intent Sale] で自動請求されると、製品のダウンロードリンクを使用できなくなります

ACSD-49843 パッチは、[!UICONTROL Payment Action] が [!UICONTROL Intent Sale] に設定されている場合に、オンライン支払い方法によって注文品目の自動請求が行われると、製品のダウンロードリンクが使用できなくなる問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.37 がインストールされている場合に使用できます。 パッチ ID は ACSD-49843 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.3.7-p4、2.4.1 ～ 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!UICONTROL Payment Action] が [!UICONTROL Intent Sale] に設定されている場合、オンライン支払い方法によって注文品目に自動請求が行われると、製品のダウンロードリンクは使用できなくなります。

<u> 再現手順 </u>:

1. Adobe Commerce管理者にログインし、**[!UICONTROL Stores]** / **[!UICONTROL Configuration]** / **[!UICONTROL Sales]** / **[!UICONTROL Configure Braintree]** に移動します。

   * [!UICONTROL Payment Action] ドロップダウンで「**[!UICONTROL Intent Sale]**」を選択し、「*[!UICONTROL Enable Card Payments]*」を *はい* に設定します。

1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Downloadable Product Option]**/**[!UICONTROL Order Item status for Download]** に移動し、*「請求済み」* に設定されていることを確認します。
1. ストアフロントで、顧客としてログインします。

   * ダウンロード可能な製品とシンプルな製品を買い物かごに追加します。
   * [!DNL Braintree Pay] を使用して、カード オプションを使用して注文します。

1. **[!UICONTROL My Orders]** に移動して、注文に対する請求書が自動的に作成され、両方の品目ステータスが「請求済 *であることを確認し* す。
1. **[!UICONTROL My Downloadable Products]** に移動し、ダウンロードリンクがまだ使用できないことを確認します。
1. 管理者で、その注文に移動し、その注文の出荷を作成します。
1. ストアフロントで、**[!UICONTROL My Downloadable Products]** に移動して、ダウンロードリンクが使用可能になったことを確認します。

<u> 期待される結果 </u>:

ダウンロードリンクは、ダウンロード可能な製品ステータスが *「請求済み」の場合に使用* きます。

<u> 実際の結果 </u>:

ダウンロード可能な製品ステータスが「請求済み *と表示されている場合でも、ダウンロードリンクは使用* きません。 物理的な製品の出荷が作成された後にのみ使用できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
