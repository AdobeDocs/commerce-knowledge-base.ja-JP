---
title: 「ACSD-52714:y-m-d として設定されている場合、日付フィルターが管理グリッドで機能しない」
description: ACSD-52714 パッチを適用すると、日付フォーマットが y-m-d に設定されている場合に、管理グリッドで日付フィルターが機能しないAdobe Commerceの問題が修正されます。
feature: Attributes
role: Admin, Developer
exl-id: b292ab2c-e12d-40df-a9ad-19f25fbde5a0
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# ACSD-52714:y-m-d として設定されている場合、管理グリッドで日付フィルターが機能しない

ACSD-52714 パッチでは、日付形式が y-m-d に設定されている場合に、管理グリッドで日付フィルターが機能しない問題が修正されています。このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされています。 パッチ ID は ACSD-52714 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

日付形式が y-m-d に設定されている場合、管理グリッドでは日付フィルターが機能しません。

<u>再現手順</u>:

1. クリーンなAdobe Commerceをインストールします。
1. 編集
   `/app/code/Magento/Customer/view/adminhtml/ui_component/customer_listing.xml`
ファイルと追加
   `<dateFormat>Y-MM-dd</dateFormat>`
対象：
   `<column name="created_at" class="Magento\Ui\Component\Listing\Columns\Date" component="Magento_Ui/js/grid/columns/date" sortOrder="100">`
タグの下
   `<dataType>date</dataType>`

1. キャッシュをフラッシュします `bin/magento c:f`.
1. 管理者にログインし、から新しい顧客を作成する **[!UICONTROL Customers]** > **[!UICONTROL All Customers]**.

   * 開始日：現在の日付 – 1 日
   * 終了日：現在の日付

1. クリックする **[!UICONTROL Apply Filters]**.

<u>期待される結果</u>:

グリッドの日付フィルターは、ロケールの設定に関係なく正しく機能します。

<u>実際の結果</u>:

次のメッセージが表示されます。 *レコードが見つかりませんでした*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
