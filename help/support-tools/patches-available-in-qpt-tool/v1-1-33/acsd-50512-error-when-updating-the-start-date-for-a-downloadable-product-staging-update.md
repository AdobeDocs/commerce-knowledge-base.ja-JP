---
title: 「ACSD-50512：ダウンロード可能な製品のステージング更新の開始日を更新する際にエラーが発生しました」
description: ダウンロード可能な製品のステージングアップデートの開始日を更新する際に、「ダウンロード可能なリンクが製品に関連していません。リンクを確認して、もう一度やり直してください」というエラーが発生するAdobe Commerceのパフォーマンスの問題を修正するために、ACSD-51892 パッチを適用します。
feature: Products, Staging
role: Admin
exl-id: 873357ef-49c3-48f8-a98e-41c48cb9ba8b
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# ACSD-50512：ダウンロード可能な製品のステージング更新の開始日を更新する際にエラーが発生しました

ACSD-50512 パッチは、エラーが発生する問題を修正します *ダウンロード可能リンクは製品に関連していません。 リンクを確認して、もう一度試してください*&#x200B;ダウンロード可能な製品のステージング更新の開始日を更新するときに発生します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.33 がインストールされています。 パッチ ID は ACSD-51502 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

エラー *ダウンロード可能リンクは製品に関連していません。 リンクを確認して、もう一度試してください*&#x200B;ダウンロード可能な製品のステージング更新の開始日を更新するときに発生します。

<u>再現手順</u>:

1. を使用したダウンロード可能な製品の作成 *ダウンロード可能なリンク* および *サンプルリンク*.
1. 同じ商品のスケジュールされた更新を作成し、商品を保存します。
1. （手順 2 で）事前設定されたスケジュール済み更新を編集し、開始日を変更します。
1. スケジュールされた更新を保存します。

<u>期待される結果</u>:

スケジュールされた更新に対する変更は正常に保存されました。

<u>実際の結果</u>:

次のエラーが発生します。 *ダウンロード可能リンクは製品に関連していません。 リンクを確認して、もう一度試してください*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
