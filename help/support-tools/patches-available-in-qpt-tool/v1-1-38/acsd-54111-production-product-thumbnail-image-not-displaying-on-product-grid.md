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

ACSD-54111 パッチにより、すべての画像がデフォルトの製品プレースホルダー画像に置き換わる問題が修正されました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.38 がインストールされています。 パッチ ID は ACSD-54111 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法）:2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法）:2.4.2 ～ 2.4.5-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品のサムネール画像が表示されない。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Content]** > **[!UICONTROL Design]** > **[!UICONTROL Configuration]** > **[!UICONTROL Edit Theme]** > **[!UICONTROL Product Image Watermarks]** > **[!UICONTROL Thumbnail]**.
1. サムネール付きの画像をアップロードし、画像の位置をに設定します。 *[!UICONTROL Center]*.
1. クリックする **[!UICONTROL Save Configuration]**.
1. キャッシュをクリアします。
1. ゲスト/顧客としてストアフロントに移動します。
1. 商品を買い物かごに追加します。
1. 実行 `bin/magento catalog:image:resize` コンソールから変更します。
1. フロントエンドのミニカートまたはバックエンドの製品グリッドを開いて、画像のサムネールが表示されているかどうかを確認します。

<u>期待される結果</u>:

製品画像はプレースホルダー画像に置き換えられません。

<u>実際の結果</u>:

製品画像は、デフォルトの製品プレースホルダー画像に置き換えられます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
