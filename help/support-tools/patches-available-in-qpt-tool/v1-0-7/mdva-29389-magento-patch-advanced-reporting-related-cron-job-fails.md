---
title: 「MDVA-29389：詳細レポートに関連する cron ジョブが失敗する」
description: 「MDVA-29389 パッチでは、「analytics_collect_data」 cronjob に「*Port must be configured within host parameter （like localhost:3306）*」と表示される詳細レポートの問題が修正されています。」 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 パッチ ID は MDVA-29389。 この問題はAdobe Commerce 2.4.2 で修正されました。'
exl-id: eee909d5-9d0d-46b6-846a-665f89db0eee
feature: Cache
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# MDVA-29389：詳細レポートに関連する cron ジョブが失敗する

MDVA-29389 パッチでは、Advanced Reporting で `analytics_collect_data` cronjob に「*Port must be configured within host parameter （like localhost:3306）*」と表示される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.7 がインストールされている場合に使用できます。 パッチ ID は MDVA-29389。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4.

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.1。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. お使いのAdobe Commerce インスタンスで、詳細レポートを有効にします。
1. 次のクエリを実行して、分析/一般/トークン値を DB に挿入します。

   ```sql
   INSERT INTO core_config_data VALUES(NULL,'default',0,'analytics/general/token','ABCDE',now());
   ```

1. env.php を開き、次の形式で DB 設定の host パラメータにポートを追加します。`'host' => 'hostname:port',`
1. キャッシュをクリアします。
1. `analytics_collect_data` cron ジョブを実行します。

<u> 期待される結果 </u>:

env.php で MySQL に接続するためにデフォルトまたは非デフォルトのポートを使用する場合、`analytics_collect_data` ジョブは正常に実行されます。

<u> 実際の結果 </u>:

env.php でデフォルト以外のポートを使用して MySQL に接続すると、`analytics_collect_data` ジョブが「*Port must be configured within host parameter （like localhost:3306）*」というエラーをスローする。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
