---
title: 「ACSD-46520：ストアクレジットを使用して払い戻した場合の注文ステータスが正しくない」
description: この記事では、ストアクレジットを使用して返金すると、ユーザーに誤った注文ステータスが表示される問題の解決策を説明します。
exl-id: 8464df22-0223-4ded-a15f-ce06eacdf77c
feature: Orders, Returns
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# ACSD-46520：ストアクレジットを使用して払い戻した際の注文ステータスが正しくない

ACSD-46520 パッチは、ストアクレジットを使用して払い戻した際に、ユーザーが誤った注文ステータスを取得する問題を解決します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.20 がインストールされている場合に使用できます。 パッチ ID は ACSD-46520 です。 この問題はAdobe Commerce 2.4.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 および 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアクレジットを使用して返金すると、ユーザーに誤った注文ステータスが表示される。

<u> 再現手順 </u>:

1. ストアフロントで顧客アカウントを作成し、ログインします。
1. 管理者から顧客にストアクレジットを割り当てます。 ストアクレジットは注文全体に適用されます。
1. 店舗クレジットを使用して注文します。
1. 注文を請求します。
1. 注文の全額を返金するクレジットメモを作成します。
「**[!UICONTROL Refund to store credit]**」チェックボックスをオンにします。
1. 注文ステータスを確認します。

<u> 期待される結果 </u>:

注文ステータスは *クローズ* です。

<u> 実際の結果 </u>:

注文ステータスが *完了* であり、これは正しいステータスではありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe Commerceまたは [!DNL Magento Open Source] オンプレミス：[Quality Patches Tool Guide の ](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html)Quality Patches Tools > Usage&rbrack;。
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/check-patch-for-magento-issue-with-magento-quality-patches.html) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細は、『品質向上パッチ ツール ガイド』の「[[!DNL Quality Patches Tool]：パッチの検索 ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
