---
title: 「ACSD-51102：多数の製品に適用されたカタログルールのインデックスが正しくない」
description: ACSD-51102 パッチを適用すると、Adobe Commerceの問題を修正できます。この問題では、スケジュールされた更新によってルールが有効になると、多数の商品に適用されるカタログルールのインデックスが正しく作成されません。
feature: Catalog Management, Products
role: Admin
exl-id: 5c1c5f9c-9cce-4b11-8058-0e12a4bf93fd
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# ACSD-51102：多数の製品に適用されているカタログルールが正しくインデックス化されていない

ACSD-51102 パッチを適用すると、スケジュールされた更新によってルールが有効にされたときに、多数の製品に適用されるカタログルールが正しくインデックス化されない問題が修正されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされています。 パッチ ID は ACSD-51102 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

スケジュールされた更新でルールが有効になっている場合、多数の製品に適用されているカタログルールのインデックスが正しく作成されません。

前提条件：

* Cron ジョブは毎分設定され実行されます。

<u>再現手順</u>:

1. の実行時間を確保するために、数千個の製品からなる大規模なカタログを作成します。 *カタログルール* カタログルールが有効になっている場合の 120 秒を超えるインデクサー。
2. を使用した 2 つのカタログルールの作成 *アクティブ* ステータスの設定先 *不可*.  例： *テスト 1* および *テスト 2*. 各ルールはカタログ内のすべての製品に影響し、インデクサーが 120 秒以上実行される必要があります。
3. インデクサーのステータスがであることを確認します。 *準備完了*.
4. スケジュールされた更新を作成して、これら 2 つのルールを有効にします。 *テスト 2* スケジュールは、の直後に開始されます *テスト 1*. 例えば、1 分の差があるとします。
5. ストアフロントにて商品価格をご確認ください。

<u>期待される結果</u>

両方のルールの割引が適用されます。

<u>実際の結果</u>

最初のルールの割引のみが適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
