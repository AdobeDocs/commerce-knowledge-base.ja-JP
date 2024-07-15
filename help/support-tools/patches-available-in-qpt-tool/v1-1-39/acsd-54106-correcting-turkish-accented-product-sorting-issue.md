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

ACSD-54106 パッチでは、トルコ語のアクセント付き文字に対してカテゴリ製品を名前で並べ替えると誤って表示される問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.39 がインストールされている場合に使用できます。 パッチ ID は ACSD-54106 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.4-p5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カテゴリ内の製品を名前で並べ替えると、トルコ語のアクセント記号付き文字に対して正しく表示されません。

<u> 再現手順 </u>:

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
1. 並べ替え順を *[!UICONTROL By Name]* に変更します。

<u> 期待される結果 </u>:

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

<u> 実際の結果 </u>:

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

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
