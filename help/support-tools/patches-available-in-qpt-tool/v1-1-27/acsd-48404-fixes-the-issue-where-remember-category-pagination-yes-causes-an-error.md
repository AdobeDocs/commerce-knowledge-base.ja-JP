---
title: 「ACSD-48404:*[!UICONTROL Remember Category Pagination] = [!UICONTROL Yes]*は、ブラウザーの戻るボタンを押すとエラーが発生する」
description: ACSD-48404 パッチを適用すると、Adobe Commerceの問題が修正されます。*[!UICONTROL Remember Category Pagination] = [!UICONTROL Yes]*では、ブラウザーの戻るボタンを押すとエラーが発生します。
exl-id: b4b96198-dee6-4b3c-b60a-0983ef8ef7b2
feature: Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# ACSD-48404:*[!UICONTROL Remember Category Pagination]=[!UICONTROL Yes]* で、ブラウザーの戻るボタンを押すとエラーが発生する

ACSD-48404 パッチでは、ブラウザーの戻るボタンを押すと *[!UICONTROL Remember Category Pagination]=[!UICONTROL Yes]* がエラーを引き起こす問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされている場合に使用できます。 パッチ ID は ACSD-48404 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.3-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

*[!UICONTROL Remember Category Pagination]=[!UICONTROL Yes]* は、ブラウザーの戻るボタンを押したときにエラーが発生します。


<u> 再現手順 </u>:

1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Storefront]** に移動し、「*[!UICONTROL Remember Category Pagination]*」を *はい* に設定します。
1. ストアフロントでカテゴリを開きます。
1. *[!UICONTROL Show Per Page]* ドロップダウンでデフォルト値以外の値を選択します。 オプションを選択すると、ページが再読み込みされます。
1. ページが再読み込みされたら、カタログページの任意の製品をクリックします。
1. 開いた製品詳細ページで、ブラウザーの「**[!UICONTROL Back]**」ボタンをクリックします。

<u> 期待される結果 </u>:

カタログページが再び開きます。

<u> 実際の結果 </u>:

カテゴリページがエラーを返します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
