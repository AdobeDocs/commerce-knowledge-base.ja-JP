---
title: 「ACSD-58054：非アクティブな顧客の API トークン生成」
description: ACSD-58054 パッチを適用すると、API を介して非アクティブなユーザーのカスタマートークンを生成できるAdobe Commerceの問題を修正できます。
feature: Customers, API Mesh
role: Admin, Developer
source-git-commit: 70f90884d8106719934b007b2e33f033e1b7e2b2
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# ACSD-58054：非アクティブな顧客の API トークン生成

ACSD-58054 パッチは、API を介して非アクティブな顧客のカスタマートークンを生成できる問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.49 がインストールされている場合に使用できます。 パッチ ID は ACSD-58054 です。 この問題は B2B 1.5.1 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p9

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

API を介した非アクティブな顧客トークン生成。

<u> 前提条件 </u>:

B2B モジュールがインストールされます。

<u> 再現手順 </u>:

1. 顧客アカウントを作成します。
1. API を使用して顧客トークンを作成します。
1. バックエンドに移動し、顧客アカウントを無効にします。
1. もう一度顧客トークンを生成してみてください。

<u> 期待される結果 </u>:

トークンは生成されません。

<u> 実際の結果 </u>:

トークンが生成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
