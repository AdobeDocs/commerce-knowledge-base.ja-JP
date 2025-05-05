---
title: '「ACSD-50895: [!DNL Google Analytics] 3 GTM が設定されていない場合、GTM タグが実行され  [!DNL Google Analytics]  せん」'
description: ' [!DNL Google Analytics] 4 GTM が設定されていない場合、 [!DNL Google Analytics] 3 GTM タグが実行されないAdobe Commerceの問題を修正するために、ACSD-50895 パッチを適用します。'
role: Admin
exl-id: da48f6f1-a68b-4a9c-a79a-d7bd01b65dc2
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# ACSD-50895:[!DNL Google Analytics] 3 GTM が設定されていない場合、[!DNL Google Analytics] 4 GTM タグが実行されない

ACSD-50895 パッチは、[!DNL Google Analytics] 4 GTM が設定されていない場合に [!DNL Google Analytics] 3 GTM タグが起動されない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-50895 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL Google Analytics] 3 GTM が設定されていない場合、[!DNL Google Analytics] 4 GTM タグは実行されません。

<u> 再現手順 </u>:

1. 管理者ユーザーとしてログインします。
1. **Admin**/**Store**/**Configuration**/**Sales**/10&rbrace;Google API **/** Google Analytics **で、**&#x200B;[!DNL Google Analytics 3]&#x200B;**と&#x200B;**&#x200B;[!DNL Google Tag Manager]&#x200B;**を有効にします。**
1. **[!DNL Google Analytics 4]** と **[!DNL Google Tag Manager]** を有効にしないでください。
1. ストアフロントの商品ページを開きます。

<u> 期待される結果 </u>:

GTM タグは、**[!DNL Google Analytics]** 3 GTM のみが有効な場合に実行されます。

<u> 実際の結果 </u>:

**[!DNL Google Analytics]** 4 GTM が無効になっている場合、GTM タグは実行されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
