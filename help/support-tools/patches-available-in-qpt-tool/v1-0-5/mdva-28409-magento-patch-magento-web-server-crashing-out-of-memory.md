---
title: 「MDVA-28409 パッチ：Adobe Commerce web サーバーのクラッシュ – メモリ不足」
description: MDVA-28409 パッチでは、多数の項目を処理する必要があるため、引用符を削除する cron ジョブが停止する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） v.1.0.5 がインストールされている場合に利用できます。
exl-id: 175e5f2f-2f76-42ee-83e9-c1b23ff81e96
feature: Tools and External Services
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# MDVA-28409 パッチ：Adobe Commerce Web サーバーのクラッシュ – メモリ不足

MDVA-28409 パッチでは、多数の項目を処理する必要があるため、引用符を削除する cron ジョブが停止する問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) v.1.0.5 がインストールされている。

## 影響を受ける製品とバージョン

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.4 - 2.3.5、2.4.0

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この問題は、ジョブが処理しようとしているデータ量が原因で、cron ジョブがメモリ不足になったことです。 この問題の症状には、MySQL によるディスク使用量が多く、web サーバーのメモリが少ないことが原因でパフォーマンスが低下することが含まれます。

<u>再現手順：</u>

古い引用符を削除できない cron ジョブがあるかどうかを確認するには、次のクエリを実行します。

```
select * from cron_schedule where job_code like '%sales_clean_quotes%'
```

<u>期待される結果：</u>

ステータス `sales_clean_quotes` cron ジョブは `success`.

<u>実際の結果：</u>

ステータス `sales_clean_quotes` cron ジョブはです `running` または `error`.

古い引用符を削除できない cron ジョブがあることを確認するもう 1 つの方法は、クエリから出力をマッピングすることです。 **手順 1** （`executed_at`）に表示されます。使用されるのは、のメモリエラーのタイムスタンプです。 `/var/log/cron.log`. データ量を処理できない cron ジョブがある場合は、次のようなメッセージが表示される場合があります。

```
PHP Fatal error:  Allowed memory size of 1073741824 bytes exhausted (tried to allocate 4096 bytes) in /app/vendor/magento/framework/DB/Statement/Pdo/Mysql.php on line 91

Fatal error: Allowed memory size of 1073741824 bytes exhausted (tried to allocate 4096 bytes) in /app/vendor/magento/framework/DB/Statement/Pdo/Mysql.php on line 91
--
[2020-05-30 05:00:27.224718] Launching command 'php bin/magento cron:run'.
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
