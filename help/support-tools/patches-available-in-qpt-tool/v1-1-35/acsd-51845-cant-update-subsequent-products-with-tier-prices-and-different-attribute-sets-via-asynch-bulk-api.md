---
title: 「ACSD-51845：非同期一括を使用して、階層価格と異なる属性セットを持つ後続の製品を更新できない  [!DNL API]」
description: ACSD-51845 パッチを適用すると、非同期の一括  [!DNL REST API] を使用して階層価格や異なる属性セットで後続の製品を更新できないAdobe Commerceの問題を修正できます。
feature: REST, Products
role: Admin
exl-id: c3fff9f2-30ad-4bcb-945e-e9e0c69630b3
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# ACSD-51845：非同期バルクサー [!DNL API] スを使用して、階層価格と異なる属性セットを持つ後続の製品を更新できない

ACSD-51845 パッチを適用すると、非同期の一括アップデートを使用して、階層価格や異なる属性セットで後続の製品を [!DNL REST API] 新できない問題が修正されます。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされている場合に使用できます。 パッチ ID は ACSD-51845 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

階層の価格が設定され、非同期の一括アップデートを使用して属性セットが異なる後続の製品の [!DNL REST API] 新が失敗します。

<u> 再現手順 </u>:

1. [!DNL RabbitMQ] の設定
1. 2 つの属性セットを作成します。
1. 各製品を異なる属性セットに割り当てて、2 つの **シンプルな製品** を作成します。
1. 各製品の **顧客グループ価格** を追加します。
1. 同じ一括アップデートで両方の製品 [!DNL API] アップデートします。
1. `bin/magento queue:consumers:start async.operations.all` コマンドが実行中であることを確認します。
1. 一括 [!DNL API] ールステータスを確認します。

<u> 期待される結果 </u>:

サービスが正常に実行されました。

<u> 実際の結果 </u>:

「*製品を保存できませんでした。 もう一度やり直してください。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
