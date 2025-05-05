---
title: 「ACSD-51700：ダウンロード可能な製品編集ページでのストアビューの切り替えエラー」
description: ACSD-51700 パッチを適用すると、管理者のダウンロード可能な製品編集ページでストアビューを切り替えるとエラーが発生するAdobe Commerceの問題を修正できます。
feature: Products
role: Admin
exl-id: 652876a5-275d-437f-9cb3-baf4e7b23aae
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# ACSD-51700：ダウンロード可能な製品編集ページでのストア ビューの切り替えエラー

ACSD-51700 パッチでは、管理者のダウンロード可能な製品編集ページでストアの表示を切り替えるとエラーが発生する問題を修正しています。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-51700 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 - 2.4.6-p1

## 問題

管理者のダウンロード可能な製品編集ページでストアの表示を切り替えると、エラーが発生します。

<u> 再現手順 </u>:

1. 名前、[!DNL SKU]、価格を指定してダウンロード可能な製品を作成します。 リンクを追加せずに、製品を保存します。
1. すべてのストア表示からデフォルトのストア表示に切り替えます。
1. ダウンロード可能な製品のリンクを作成して保存します。
1. デフォルトのストア表示からすべてのストア表示に切り替えます。

<u> 期待される結果 </u>:

リンクされた製品が表示されます。

<u> 実際の結果 </u>:

次のエラーが表示されます。

*非推奨の機能：number_format （）:float 型のパラメータ#1 （$num）に null を渡すことは、vendor/magento/module-downloadable/Ui/DataProvider/Product/Form/Modifier/Data/Links.phpの 228 行目で非推奨になりました*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
