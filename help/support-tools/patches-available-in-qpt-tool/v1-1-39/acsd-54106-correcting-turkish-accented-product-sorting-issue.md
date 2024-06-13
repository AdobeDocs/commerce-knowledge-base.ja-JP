---
title: 「ACSD-54106：製品カテゴリでのトルコ語アクセント付き文字の並べ替えの修正」
description: ACSD-54106 パッチを適用すると、トルコ語のアクセント付き文字に対してカテゴリ商品を名前で並べ替えるとAdobe Commerceの問題が修正されます。
feature: Categories, Products, Search
role: Admin
exl-id: 80386ded-4ada-4822-b073-f477ca123093
source-git-commit: dccb8dde1666fa0c72c7c94cd94c82daddaadc54
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# ACSD-54106：製品カテゴリでのトルコ語アクセント記号付き文字の並べ替えの修正

ACSD-54106 パッチでは、トルコ語のアクセント付き文字に対してカテゴリ製品を名前で並べ替えると誤って表示される問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.39 がインストールされています。 パッチ ID は ACSD-54106 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.4-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カテゴリ内の製品を名前で並べ替えると、トルコ語のアクセント記号付き文字に対して正しく表示されません。

<u>再現手順</u>:

1. 管理パネルにログインします。
1. 次のような名前の単純な製品を作成して、任意のカテゴリに割り当てます。

* 名前 A
* 名前 Ç
* 名前 D
* 名前
* 名前 M
* 名前
* 名前 Ü
* 名前 Y
* 名前 Z

1. ストアフロントに移動し、製品を含むカテゴリにアクセスします。
1. 並べ替え順を次のように変更します。 *[!UICONTROL By Name]*.

<u>期待される結果</u>:

商品は、次の順序で正しく並べ替えられます。

* 名前 A
* 名前 Ç
* 名前 D
* 名前
* 名前 M
* 名前
* 名前 Ü
* 名前 Y
* 名前 Z

<u>実際の結果</u>:

製品が、次の順序で正しく並べ替えられていません。

* 名前 A
* 名前 D
* 名前 M
* 名前 Y
* 名前 Z
* 名前 Ç
* 名前
* 名前 Ü
* 名前

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
