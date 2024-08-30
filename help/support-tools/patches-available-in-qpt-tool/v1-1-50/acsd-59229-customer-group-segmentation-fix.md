---
title: 「ACSD-59229：古い X-Magento-Vary 値が原因で、お客様グループのデータが誤って割り当てられている」
description: ACSD-59229 パッチを適用すると、リクエストの X-Magento-Vary 値が古くなっているために、お客様のグループ関連の情報が間違ったセグメントに保存されるAdobe Commerceの問題が修正されます。
feature: Customers, Personalization, Marketing Tools
role: Admin, Developer
source-git-commit: 41d502a85a0cbb4eb8d186e4c1e1256aec3f8740
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# ACSD-59229：古い X-Magento変動値が原因で、お客様グループのデータが誤って割り当てられている

ACSD-59229 パッチは、リクエスト内の X-Magento-Vary の値が古いために、お客様のグループ関連の情報が間違ったセグメントに保存される問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.50 がインストールされている場合に使用できます。 パッチ ID は ACSD-59229 です。 この問題は 2.4.7 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p8

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p7

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

リクエスト内の X-Magento-Vary 値が古いので、お客様グループ関連の情報が間違ったセグメントに保存される。

<u> 前提条件 </u>:

サンプルデータを含むAdobe Commerce B2B がインストールされ、[!DNL Varnish] が設定されていることを確認します。

<u> 再現手順 </u>:

1. [!DNL SKU 24-MB01] の詳細価格を設定します。
   1. [!UICONTROL Regular price] = *9999$*
   1. [!UICONTROL Catalog and Tier Price]:
      * *卸売*=200 *ドル*
      * *小売業者* = 30 *ドル*

1. 2 つの顧客アカウントを作成します。
1. 両方の顧客を **Wholesale** グループに割り当てます。
1. 2 つの異なるブラウザーセッションを開き、各顧客と共にログインします。
1. 各顧客の **[!UICONTROL 24-MB01]** 製品ページに移動し、表示されている価格が 200 *ド* であることを確認します。
1. いずれかの顧客の顧客グループを **小売** に変更します。
1. 次のコマンドを使用してキャッシュをクリアします：`bin/magento cache:flush full_page`。
1. 各顧客の製品ページを更新します。

<u> 期待される結果 </u>:

1. 小売顧客は、製品の正しい価格 *30* ドルを確認できます。
1. 卸売のお客様は、製品の正しい価格 *200* ドルを見ることができます。

<u> 実際の結果 </u>:

1. 小売顧客は、製品の正しい価格 *30* ドルを確認できます。
1. 卸売業者の顧客に、製品の 30 ** ドル（小売価格）の誤った価格が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
