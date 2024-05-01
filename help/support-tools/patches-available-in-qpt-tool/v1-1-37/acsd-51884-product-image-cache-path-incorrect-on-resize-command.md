---
title: 「ACSD-51884:resize コマンドでの製品画像のキャッシュパスが正しくない」
description: ACSD-51884 パッチを適用して、resize コマンドの実行後に product image cache path が不正確になるAdobe Commerceの問題を修正してください。
feature: Products
role: Admin
exl-id: cf542c4b-07b1-4f05-95bc-82bc098bcd4d
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# ACSD-51884:resize コマンドでの製品画像のキャッシュパスが正しくない

ACSD-51884 パッチでは、resize コマンドの実行後に製品イメージのキャッシュ パスが誤って表示される内部エラーの問題が修正されています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.37 がインストールされています。 パッチ ID は ACSD-51884 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7～2.4.7

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

resize コマンドで製品画像のキャッシュパスが正しくなくなる。

<u>再現手順</u>:

1. 新しい web サイト / ストア / ストレビューを作成します。
1. 製品を作成して両方の web サイトに割り当て、製品画像をアップロードします。
1. 新しいテーマを作成します（添付のAdobe.zip を参照）。
1. 対象： `app/design/Adobe/theme/etc/view.xml` 変更：

```
<vars module="Magento_Catalog">
           <var name="product_image_white_borders">1</var>
</vars>
```

対象：

```
<vars module="Magento_Catalog">
           <var name="product_image_white_borders">0</var>
</vars>
```

1. 以前に作成した storereview にテーマを適用します。
1. 第 2 サイトの商品ページをご確認ください。 製品画像が正しく表示されます。
1. フラッシュキャッシュの使用：
   `bin/magento cache:flush`
1. 第 2 サイトの商品ページをご確認ください。

<u>期待される結果</u>:

製品画像が正しく表示される。

<u>実際の結果</u>:

商品画像が存在しません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
