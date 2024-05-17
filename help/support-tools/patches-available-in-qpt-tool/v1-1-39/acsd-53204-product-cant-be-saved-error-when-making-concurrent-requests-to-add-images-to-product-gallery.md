---
title: 「ACSD-53204：ギャラリーに画像を追加する同時リクエストで「製品を保存できません」エラーが発生する」
description: ACSD-53204 パッチを適用すると、Adobe Commerceの問題を修正できます。rest/V1/products/&lt;sku&gt;/media エンドポイントを使用して商品ギャラリーに画像を追加するリクエストを同時に行うと、「The product cannot be saved （商品は保存できません）」エラーがスローされます。
feature: Catalog Management, Media, Products, REST
role: Admin, Developer
exl-id: dcea2621-66cf-49d1-bba6-b61c70716e84
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# ACSD-53204: &quot;*商品を保存できません*&#x200B;ギャラリーに画像を追加する同時リクエストのエラー

ACSD-53204 パッチは、の問題を修正します。*商品を保存できません*「」というエラーは、を使用して製品ギャラリーに画像を追加するリクエストを同時に行うとスローされます `rest/V1/products/<sku>/media` エンドポイント。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.39 がインストールされています。 パッチ ID は ACSD-53204 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

“*商品を保存できません*「」というエラーは、を使用して製品ギャラリーに画像を追加するリクエストを同時に行うとスローされます `rest/V1/products/<sku>/media` エンドポイント。

<u>再現手順</u>:

1. 管理パネルにログインします。
1. SKU p1 で製品を作成します。
1. に対して複数の同時リクエストを実行する `rest/V1/products/<sku>/media` 複数の画像を同時にアップロードするためのエンドポイント。

<u>期待される結果</u>:

画像はエラーなしで保存されます。

<u>実際の結果</u>:

“*商品を保存できません*「エラーが返されるタイミングは異なります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
