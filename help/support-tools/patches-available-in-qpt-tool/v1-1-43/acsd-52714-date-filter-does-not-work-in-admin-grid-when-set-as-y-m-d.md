---
title: 「ACSD-52714:y-m-d として設定されている場合、日付フィルターが管理グリッドで機能しない」
description: ACSD-52714 パッチを適用すると、日付フォーマットが y-m-d に設定されている場合に、管理グリッドで日付フィルターが機能しないAdobe Commerceの問題が修正されます。
feature: Attributes
role: Admin, Developer
exl-id: b292ab2c-e12d-40df-a9ad-19f25fbde5a0
source-git-commit: 513cb47c054dbb907810bbdc3d20d2aca9d5e42b
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# ACSD-52714:y-m-d として設定されている場合、管理グリッドで日付フィルターが機能しない

ACSD-52714 パッチでは、日付形式が y-m-d に設定されている場合に、管理グリッドで日付フィルターが機能しない問題が修正されています。このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされている場合に使用できます。 パッチ ID は ACSD-52714 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

日付形式が y-m-d に設定されている場合、管理グリッドでは日付フィルターが機能しません。

<u> 再現手順 </u>:

1. クリーンなAdobe Commerceをインストールします。
1. 編集
   `/app/code/Magento/Customer/view/adminhtml/ui_component/customer_listing.xml`
ファイルと追加
   `<dateFormat>Y-MM-dd</dateFormat>`
対象：
   `<column name="created_at" class="Magento\Ui\Component\Listing\Columns\Date" component="Magento_Ui/js/grid/columns/date" sortOrder="100">`
タグの下
   `<dataType>date</dataType>`

1. キャッシュ `bin/magento c:f` をフラッシュします。
1. 管理者にログインし、**[!UICONTROL Customers]**/**[!UICONTROL All Customers]** から新しい顧客を作成します。

   * 開始日：現在の日付 – 1 日
   * 終了日：現在の日付

1. 「**[!UICONTROL Apply Filters]**」をクリックします。

<u> 期待される結果 </u>:

グリッドの日付フィルターは、ロケールの設定に関係なく正しく機能します。

<u> 実際の結果 </u>:

*レコードが見つかりませんでした* というメッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
