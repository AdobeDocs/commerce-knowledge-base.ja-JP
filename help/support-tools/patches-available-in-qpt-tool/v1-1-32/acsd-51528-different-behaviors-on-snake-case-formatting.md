---
title: 「ACSD-51528:snake_case 形式の異なる動作」
description: ACSD-51528 パッチを適用して、snake_case 形式で異なる動作が発生するAdobe Commerceの問題を修正してください。
exl-id: dd878321-8032-41f3-8dcd-acb0cc023b44
feature: Variables
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# ACSD-51528: snake_case 形式の異なる動作

ACSD-51528 パッチは、snake_case 形式の様々な動作を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされています。 パッチ ID は ACSD-51528 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

snake_case フォーマット設定の異なる動作。

<u>再現手順</u>:

1. のテスト `\Magento\Framework\Api\DataObjectHelper::populateWithArray` 様々なプロパティ名を持つ関数。
1. のような名前のプロパティ *NewPName* ～に変えるべきである *new_p_name*&#x200B;代わりに、に変換されます *new_pname*.
1. また、 *getNewPName* オブジェクトの関数 *ヌル* は、以下の理由で返されます *抽象モデル* は呼び出しをに正しく変換します *new_p_name* 両方の機能を相互に互換性がないようにします。

<u>期待される結果</u>

この **[!UICONTROL populateWithArray]** 関数はオブジェクトのプロパティを snake_case に正しく変換し、 **[!DNL AbstractModel's]** `Getters` および `Setters`.

<u>実際の結果</u>

使用する場合 **[!UICONTROL populateWithArray]** 関数を使用すると、名前に 2 つ以上の大文字が含まれるオブジェクトプロパティにより、最終的なデータ配列で snake_case 変換が正しく行われなくなります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
