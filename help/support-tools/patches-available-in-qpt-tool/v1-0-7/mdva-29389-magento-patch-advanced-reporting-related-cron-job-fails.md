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

MDVA-29389 パッチは、高度なレポートで次の場所にある問題を修正します。 `analytics_collect_data` cronjob は次のように述べています。*ポートは、ホストパラメーター（localhost:3306 など）内で設定する必要があります*」と入力します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。 パッチ ID は MDVA-29389。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4.

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.1。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. お使いのAdobe Commerce インスタンスで、詳細レポートを有効にします。
1. 次のクエリを実行して、分析/一般/トークン値を DB に挿入します。

   ```sql
   INSERT INTO core_config_data VALUES(NULL,'default',0,'analytics/general/token','ABCDE',now());
   ```

1. env.php を開き、次の形式で DB 設定のホストパラメーターにポートを追加します。 `'host' => 'hostname:port',`
1. キャッシュをクリアします。
1. を実行 `analytics_collect_data` cron ジョブ。

<u>期待される結果</u>:

この `analytics_collect_data` env.php で MySQL に接続するためにデフォルトまたは非デフォルトのポートを使用している場合、ジョブは正常に実行されます。

<u>実際の結果</u>:

この `analytics_collect_data` ジョブがエラー「」をスロー&#x200B;*ポートは、ホストパラメーター（localhost:3306 など）内で設定する必要があります*&#x200B;デフォルト以外のポートを使用して env.php の MySQL に接続する場合。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
