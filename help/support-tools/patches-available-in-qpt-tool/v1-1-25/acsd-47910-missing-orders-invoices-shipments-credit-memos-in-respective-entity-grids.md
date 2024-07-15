---
title: 「ACSD-47910：各エンティティ・グリッドの受注、請求書、出荷およびクレジット・メモが欠落している」
description: ACSD-47910 パッチを適用すると、それぞれのエンティティグリッドに注文、請求書、出荷、およびクレジットメモがないAdobe Commerceの問題を修正できます。
exl-id: 4eb897ec-16e4-420e-89a6-c8f7c8740303
feature: Admin Workspace, Invoices, Orders, Returns, Shipping/Delivery
role: Admin
source-git-commit: 3eeb86c2644f8a04ddcf5e205bc400d2ca9969af
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# ACSD-47910：各エンティティ・グリッドに受注、請求書、出荷およびクレジット・メモが欠落しています

ACSD-47910 パッチは、各エンティティグリッドに注文、請求書、出荷、およびクレジットメモがない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされている場合に使用できます。 パッチ ID は ACSD-47910 です。 この問題が修正されるバージョンは、まだ利用できません。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p1

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

各エンティティ・グリッドに受注、請求書、出荷およびクレジット・メモが欠落しています。

<u> 再現手順 </u>:

1. **[!UICONTROL Stores]**/**[!UICONTROL Settings]**/**[!UICONTROL Configuration]**/**[!UICONTROL Advanced]**/**[!UICONTROL Developer]**/**[!UICONTROL Grid Settings]** で **[!UICONTROL Asynchronous indexing]** を有効にします。
1. 注文を 2 回行います。
1. cron を実行して、これらの注文をグリッドに同期します。
1. 注文の 1 つを開き、請求する準備を整えます。 まだ請求書を送信しないでください。
1. フロントエンドに配置する準備ができている新しい注文を作成します。 [PLACE ORDER] ボタンはまだクリックしないでください。
1. `NotSyncedDataProvider::L43` の `foreach` に `sleep(30)` を追加します。
1. `bin/magento cron:run` を実行します。
1. 次に、新しい注文を行います。
1. 以前の注文を請求します。
1. 新しい注文が同期されることを期待して、cron を再度実行します。
1. 管理の注文グリッドに移動します。

<u> 期待される結果 </u>:

新しいオーダーがオーダーグリッドに表示されます。

<u> 実際の結果 </u>:

前回の注文の更新がグリッドに同期されました（**[!UICONTROL status: Processing]**）。 新しい注文はグリッドに表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
