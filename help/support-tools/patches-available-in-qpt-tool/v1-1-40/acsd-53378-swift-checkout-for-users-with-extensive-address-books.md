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

ACSD-53378 パッチは、顧客アドレスのボリュームが大きいためにパフォーマンスの問題が発生する問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされています。 パッチ ID は ACSD-53378 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

お客様のアドレス数が多いと、Adobe Commerceのパフォーマンスが非常に遅くなります。

設定オプション *[!UICONTROL Enable search address]* 未満 **[!UICONTROL Sales]** > **[!UICONTROL Checkout]** > **[!UICONTROL Checkout Options]** がアクティブ化されると、完全な顧客アドレス帳は完全に処理されなくなります。 処理される顧客アドレスの数は、設定によって決まります *[!UICONTROL Customer Addresses Limit]* 未満  **[!UICONTROL Sales]** > **[!UICONTROL Checkout]** > **[!UICONTROL Checkout Options]**.

<u>再現手順</u>:

1. 管理者からシンプルな製品を作成します。
1. 1000 件のアドレスを含む広範なアドレス帳を持つ顧客を作成します。
1. フロントエンドに移動し、商品を買い物かごに追加します。
1. 買い物かごページを開きます。

<u>期待される結果</u>:

顧客のアドレス数は、応答時間には影響しません。

<u>実際の結果</u>:

買い物かごページの読み込みに時間がかかる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
