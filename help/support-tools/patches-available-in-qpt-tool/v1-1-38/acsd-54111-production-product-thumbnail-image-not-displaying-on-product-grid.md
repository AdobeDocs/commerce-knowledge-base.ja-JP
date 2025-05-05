---
title: 「ACSD-54111：製品のサムネール画像が表示されない」
description: ACSD-54111 パッチを適用すると、Adobe Commerceの問題を修正できます。この問題では、すべての画像がデフォルトの製品プレースホルダー画像に置き換えられます。
feature: Products
role: Admin, Developer
exl-id: 087786e3-9d61-4fef-8884-8d22fa9170e3
source-git-commit: a863015920917050106ed5d210d0511515807cc7
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# ACSD-54111：製品のサムネール画像が表示されない

ACSD-54111 パッチにより、すべての画像がデフォルトの製品プレースホルダー画像に置き換わる問題が修正されました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.38 がインストールされている場合に使用できます。 パッチ ID は ACSD-54111 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法）:2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法）:2.4.2 ～ 2.4.5-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品のサムネール画像が表示されない。

<u> 再現手順 </u>:

1. **[!UICONTROL Content]**/**[!UICONTROL Design]**/**[!UICONTROL Configuration]**/**[!UICONTROL Edit Theme]**/**[!UICONTROL Product Image Watermarks]**/**[!UICONTROL Thumbnail]** に移動します。
1. サムネール付きの画像をアップロードし、画像の位置を *[!UICONTROL Center]* に設定します。
1. 「**[!UICONTROL Save Configuration]**」をクリックします。
1. キャッシュをクリアします。
1. ゲスト/顧客としてストアフロントに移動します。
1. 商品を買い物かごに追加します。
1. コンソールから `bin/magento catalog:image:resize` を実行します。
1. フロントエンドのミニカートまたはバックエンドの製品グリッドを開いて、画像のサムネールが表示されているかどうかを確認します。

<u> 期待される結果 </u>:

製品画像はプレースホルダー画像に置き換えられません。

<u> 実際の結果 </u>:

製品画像は、デフォルトの製品プレースホルダー画像に置き換えられます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
