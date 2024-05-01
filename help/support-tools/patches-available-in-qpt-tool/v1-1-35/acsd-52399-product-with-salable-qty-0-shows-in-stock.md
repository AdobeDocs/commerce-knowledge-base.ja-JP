---
title: 「ACSD-52399：販売可能な数量 0 の製品が在庫を示す」
description: ACSD-52399 パッチを適用すると、販売可能数量が 0 の設定可能な商品オプションが商品ページに「在庫あり」と表示されるAdobe Commerceの問題が修正されます。
feature: Products, Configuration
role: Admin, Developer
exl-id: 3c9e6edd-f7ce-492e-b74f-68354d8e2633
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# ACSD-52399：販売可能な数量 0 の製品が在庫として表示されます

ACSD-52399 パッチは、販売可能数量がゼロ（0）の設定可能な製品オプションが表示される問題を修正します *在庫あり* 製品ページに移動します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-52399 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.5-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

販売可能数量がゼロ（0）の設定可能な製品オプションは、次を示します *在庫あり* 製品ページに移動します。

<u>再現手順</u>:

1. ゼロ（0）の販売可能数量の製品オプションを使用して、設定可能な製品を作成します。
1. ストアフロントの製品ページに移動し、設定可能な製品を選択して、バリエーション/設定を確認します。
1. を選択 **[!UICONTROL Add to Cart]**.

<u>期待される結果</u>:

*[!UICONTROL Add to Cart]* 選択時にボタンが使用できない *在庫切れ* 製品の設定。

<u>実際の結果</u>:

設定可能なバリエーションはストアフロントで使用でき、選択して買い物かごに追加できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
