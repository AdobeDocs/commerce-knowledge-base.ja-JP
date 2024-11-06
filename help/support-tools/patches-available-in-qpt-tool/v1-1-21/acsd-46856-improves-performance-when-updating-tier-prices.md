---
title: 「ACSD-46856：階層価格を更新するとパフォーマンスが向上する」
description: System &gt；設定&gt; Import &gt; Advanced Pricing を使用して階層価格を更新する際に、パフォーマンスを向上させるために ACSD-46856 パッチを適用します。
exl-id: c08560ef-94fa-4be4-9c59-d4b1b5e4186f
feature: Orders
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# ACSD-46856: システム /設定/ インポート /詳細価格を使用した階層価格の更新が遅い

**[!UICONTROL System]**/**[!UICONTROL Configuration]**/**[!UICONTROL Import]**/**[!UICONTROL Advanced Pricing]** を使用して階層の価格を更新する際、ACSD-46856 パッチによりパフォーマンスが向上します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.21 がインストールされている場合に使用できます。 パッチ ID は ACSD-46856 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

**[!UICONTROL System]**/**[!UICONTROL Configuration]**/**[!UICONTROL Import]**/**[!UICONTROL Advanced Pricing]** を使用した階層価格の更新が遅い。

<u> 再現手順 </u>:

* **システム**/**設定**/**インポート**/**詳細価格** から、多数の製品（例：10k+または 20k+）をインポートします。

<u> 期待される結果 </u>:

パッチを使用すると、200,000 以上の製品の処理時間は約 1:00 分になります。

<u> 実際の結果 </u>:

パッチを適用しない場合、10k 以上の製品の処理時間は約 10:00 分です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
