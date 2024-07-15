---
title: 「ACSD-48212：製品の読み込みによって製品が間違ったソースに割り当てられる」
description: 製品の読み込みによって製品が誤ったソースに割り当てられるAdobe Commerceの問題を修正するには、ACSD-48212 パッチを適用してください。
exl-id: b3426f62-f73a-4b76-8e0e-544a9133720f
feature: Admin Workspace, Data Import/Export, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# ACSD-48212：製品のインポートによって製品が誤ったソースに割り当てられる

ACSD-48212 パッチは、製品の読み込みによって製品が誤ったソースに割り当てられる問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされている場合に使用できます。 パッチ ID は ACSD-48212 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品の読み込みによって、製品が誤ったソースに割り当てられる。

<u> 再現手順 </u>:

1. サブ在庫ソースを作成します。
1. デフォルトの在庫ソースのみを持つ製品を作成します。
1. 商品を書き出します。
1. `bin/magento cron:run` を実行します。
1. **[!UICONTROL Catalog]**/**[!UICONTROL Prdoucts]** を開きます。
1. グリッドから製品を選択します。
1. *[!UICONTROL mass action]* メニューを使用して在庫を割り当て解除します。
1. `bin/magento cron:run` を実行します。
1. *[!UICONTROL mass action]* メニューを使用してセカンダリソースを割り当てます。
1. `bin/magento cron:run` を実行します。
1. *[!UICONTROL mass action]* メニューを使用して商品を削除します。
1. `bin/magento cron:run` を実行します。
1. 以前に書き出した CSV を使用して製品を読み込みます。
1. ソース割り当てを確認します。

<u> 期待される結果 </u>:

製品は、デフォルトソースにのみ割り当てられます。

<u> 実際の結果 </u>:

製品は、デフォルトとセカンダリの両方のソースに割り当てられます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
