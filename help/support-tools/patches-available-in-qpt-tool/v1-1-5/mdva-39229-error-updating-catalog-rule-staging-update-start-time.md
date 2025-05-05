---
title: 「MDVA-39229：カタログルールのステージングの更新開始時刻を更新後にエラーが発生しました」
description: MDVA-39229 パッチでは、カタログルールのステージング更新の開始時刻を更新した後にユーザーにエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/patches/overview） 1.1.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-39229。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: b9a203af-693d-4253-877b-591ae5f388d3
feature: Catalog Management, Staging
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# MDVA-39229: カタログ ルール ステージング更新開始時刻の更新後にエラーが発生しました

MDVA-39229 パッチでは、カタログルールのステージング更新の開始時刻を更新した後にユーザーにエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/patches/overview)1.1.5 がインストールされている場合に使用できます。 パッチ ID は MDVA-39229。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.3.4-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カタログルールのステージング更新の開始時刻を更新すると、エラーが発生します。

<u> 再現手順 </u>:

1. カタログ価格ルールを作成します。
1. ステージング更新を作成して実行します。
1. クエリを実行し、ステージングフラグが作成されたことを確認します。


   `select * from flag;`


1. 新しいステージング更新を作成して、5 分後に開始します。
1. **コンテンツ**/**ステージング**/**ダッシュボード**/**新規更新** を開き、開始時刻を 1 分遅らせます。
1. 6 分待ちなさい。
1. cron を実行します。

<u> 期待される結果 </u>:

更新開始時刻が変更され、更新が適用されます。 古い更新は `staging_update` テーブルから削除されます。

<u> 実際の結果 </u>:

ユーザーに次のエラーが表示されます。

*report.ERROR: Cron ジョブ staging_synchronize_entities_period にエラーがあります：アクティブな更新は削除できません。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
