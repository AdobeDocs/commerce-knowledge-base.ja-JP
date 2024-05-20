---
title: '''ACSD-54776：未チェック [!UICONTROL Use Default Value] また、デフォルト以外の製品フィールド値は、2 番目の web サイト、ストア、ストア表示では保存されません。'
description: がオフになっているAdobe Commerceの問題を修正するには、ACSD-54776 パッチを適用します [!UICONTROL Use Default Value] また、デフォルト以外の製品フィールドの値は、2 番目の web サイト、ストア、ストアの表示では保存されません。
feature: Products
role: Admin, Developer
exl-id: 5bdad804-8d7b-48b4-ba3b-c2d5387ef55e
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# ACSD-54776：未チェック *[!UICONTROL Use Default Value]* およびデフォルト以外の製品フィールドの値は保存されません

>[!NOTE]
>
>このパッチは、 [ACSD-51984](/help/support-tools/patches-available-in-qpt-tool/v1-1-35/acsd-51984-unchecked-used-default-value-and-non-default-product-field-values-are-not-saved.md) qpt 1.1.35 でリリースされたパッチ。

ACSD-54776 パッチは、がチェックされていない問題を修正します **[!UICONTROL Use Default Value]** また、デフォルト以外の製品フィールドの値は、2 番目の web サイト、ストア、ストアの表示では保存されません。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.39 がインストールされています。 パッチ ID は ACSD-54776 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p4、2.4.6 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

未チェック *[!UICONTROL Use Default Value]* また、デフォルト以外の製品フィールドの値は、2 番目の web サイト、ストア、ストアの表示では保存されません。

<u>再現手順</u>:

1. バックエンドに移動し、に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL All Stores]** 新しい web サイト、ストア、ストア表示を作成します。
1. に移動 **[!UICONTROL Catalog]** > **[!UICONTROL Products]**&#x200B;で簡単な製品を作成して保存し、から両方の web サイトに製品を割り当てます **[!UICONTROL Product in Websites]**.
1. 手順 2 で新しく作成したストア表示に範囲を変更します。
1. に移動 **[!UICONTROL Search Engine Optimization]** 「」をオフにします **[!UICONTROL Use Default Value]** のチェックボックス [!UICONTROL Meta Title], [!UICONTROL Meta Keywords]、および [!UICONTROL Meta Description].
1. フィールドからテキストを消去します。 *[!UICONTROL Meta Title]*, *[!UICONTROL Meta Keywords]* および *[!UICONTROL Meta Description]*&#x200B;を選択し、 **[!UICONTROL Save]**.
1. に移動 **[!UICONTROL Search Engine Optimization]** また。

<u>期待される結果</u>

フィールドとチェックボックスの値が保存されます。

<u>実際の結果</u>

フィールドとチェックボックスの値は保存されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
