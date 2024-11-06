---
title: 「ACSD-48262:[!UICONTROL Allow All Products Per Page] が [!UICONTROL Yes] に設定されている場合、ストアフロントに製品が表示されない」
description: '[!UICONTROL Allow All Products Per Page] 設定が [!UICONTROL Yes] に設定されている場合にストアフロントに商品が表示されないAdobe Commerceの問題を修正するために、ACSD-48262 パッチを適用してください。'
exl-id: 327cad03-441d-4adb-8a10-802f06d3fcd1
feature: Admin Workspace, Cache, Categories, Orders, Products, Storefront
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# ACSD-48262:[!UICONTROL Allow All Products Per Page] が *[!UICONTROL Yes]* に設定されている場合、ストアフロントに製品が表示されない

[!UICONTROL Allow All Products Per Page] 設定が *[!UICONTROL Yes]* に設定されている場合、ACSD-48262 パッチにより、ストアフロントに製品が表示されない問題が修正されました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされている場合に使用できます。 パッチ ID は ACSD-48262 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） >=2.4.5 &lt; 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!UICONTROL Allow All Products Per Page] 設定が *[!UICONTROL Yes]* に設定されている場合、ACSD-48262 パッチにより、ストアフロントに製品が表示されない問題が修正されました。

<u> 再現手順 </u>:

1. テストカテゴリを作成します。
1. テストカテゴリでテスト製品を作成します。
1. 製品を参照してストアフロントのカテゴリページをテストし、製品が表示されていることを確認します。
1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]** に移動し、[!UICONTROL Allow All Products Per Page] 設定を *[!UICONTROL Yes]* に設定します。
1. キャッシュをクリアします。
1. ストアフロントのカテゴリページをご確認ください。

<u> 期待される結果 </u>:

商品が表示されます。

<u> 実際の結果 </u>:

商品が表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。


## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
