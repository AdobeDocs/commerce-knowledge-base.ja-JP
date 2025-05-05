---
title: 「ACSD-53378：広範なアドレス帳を持つお客様のチェックアウトエクスペリエンスの向上」
description: ACSD-53378 パッチを適用して、カスタマーアドレスのボリュームが多いためにパフォーマンスの問題が発生するAdobe Commerceの問題を修正します。
feature: Customers, Checkout
role: Admin
exl-id: 561462fd-844b-40e0-9ccd-25f7aa9be161
source-git-commit: 35cd21581ee34a6213be42a79e159439b8856fb6
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# ACSD-53378：広範なアドレス帳を持つお客様のチェックアウトエクスペリエンスの強化

ACSD-53378 パッチは、顧客アドレスのボリュームが大きいためにパフォーマンスの問題が発生する問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされている場合に使用できます。 パッチ ID は ACSD-53378 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

お客様のアドレス数が多いと、Adobe Commerceのパフォーマンスが非常に遅くなります。

**[!UICONTROL Sales]**/**[!UICONTROL Checkout]**/**[!UICONTROL Checkout Options]** の設定オプション *[!UICONTROL Enable search address]* が有効になっている場合、顧客アドレス帳全体の処理は行われなくなります。 処理される顧客アドレスの数は、**[!UICONTROL Sales]**/**[!UICONTROL Checkout]**/**[!UICONTROL Checkout Options]** の設定 *[!UICONTROL Customer Addresses Limit]* によって決まります。

<u> 再現手順 </u>:

1. 管理者からシンプルな製品を作成します。
1. 1000 件のアドレスを含む広範なアドレス帳を持つ顧客を作成します。
1. フロントエンドに移動し、商品を買い物かごに追加します。
1. 買い物かごページを開きます。

<u> 期待される結果 </u>:

顧客のアドレス数は、応答時間には影響しません。

<u> 実際の結果 </u>:

買い物かごページの読み込みに時間がかかる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
