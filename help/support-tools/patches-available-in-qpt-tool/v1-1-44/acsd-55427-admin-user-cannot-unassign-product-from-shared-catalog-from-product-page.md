---
title: 「ACSD-55427：管理者が製品ページの**[!UICONTROL Product in Shared Catalogs]**から製品の割り当てを解除できない」
description: ACSD-55427 パッチを適用して、**[!UICONTROL Product in Shared Catalogs]**から商品の割り当てを解除できないAdobe Commerceの問題を修正してください。
feature: Products, B2B
role: Admin, Developer
exl-id: 1e08def1-07f6-42e0-b600-9f0bfdd6477a
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# ACSD-55427：管理者が製品ページの **[!UICONTROL Product in Shared Catalogs]** から製品の割り当てを解除できない

ACSD-55427 パッチでは、Commerce Admin のカタログ内の製品ページの **[!UICONTROL Product in Shared Catalogs]** から製品の割り当てを解除できない問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.44 がインストールされている場合に使用できます。 パッチ ID は ACSD-55427 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Commerce Admin のカタログにある製品のページで、**[!UICONTROL Product in Shared Catalogs]** から製品の割り当てを解除することはできません。

<u> 再現手順 </u>:

前提条件：B2B と **[!UICONTROL Shared Catalogs]** の両方が有効な状態でAdobe Commerceがインストールされていること。
1. 商品を作成します。
1. 共有カタログダッシュボードに移動し、デフォルトの共有カタログを開きます。
1. 製品をデフォルトのカタログに割り当て、製品価格よりも低い価格を設定します。
1. 共有カタログを保存します。
1. [!UICONTROL CRON] を実行して、コンシューマー/インデクサーを更新します。
1. 製品を開いて、「」セクションの下から製品 **[!UICONTROL Product in Shared Catalogs]** 削除します。

<u> 期待される結果 </u>:

製品は、**[!UICONTROL Product in Shared Catalogs]** のセクションのから削除する必要があります。

<u> 実際の結果 </u>:

製品は、**[!UICONTROL Product in Shared Catalogs]** のセクションに引き続き表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
