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

ACSD-50512 パッチは、エラー *ダウンロード可能なリンクは製品に関連していません。 ダウンロード可能な製品のステージング更新の開始日を更新する際に、リンクを確認して* もう一度試してください。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-51502 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

エラー *ダウンロード可能なリンクは製品に関連していません。 ダウンロード可能な製品のステージング更新の開始日を更新する際に、リンクを確認して* もう一度試してください。

<u> 再現手順 </u>:

1. *ダウンロード可能なリンク* および *サンプルリンク* を含む、ダウンロード可能な製品を作成します。
1. 同じ商品のスケジュールされた更新を作成し、商品を保存します。
1. （手順 2 で）事前設定されたスケジュール済み更新を編集し、開始日を変更します。
1. スケジュールされた更新を保存します。

<u> 期待される結果 </u>:

スケジュールされた更新に対する変更は正常に保存されました。

<u> 実際の結果 </u>:

*ダウンロード可能なリンクは製品に関連していません。 リンクを確認して、もう一度やり直してください*。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
