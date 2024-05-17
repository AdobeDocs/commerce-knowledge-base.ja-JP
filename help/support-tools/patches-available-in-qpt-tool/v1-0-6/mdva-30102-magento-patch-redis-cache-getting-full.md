---
title: 'MDVA-30102: Redis キャッシュがいっぱいです'
description: MDVA-30102 パッチは、Redis キャッシュがいっぱいになり、エラーが発生する問題を解決します。この問題により、製品リスト ページ（PLP）と製品詳細ページ（PDP）に問題が生じ、製品が見つからないなどの問題が発生します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.6 がインストールされている場合に利用できます。
exl-id: 34772296-8c93-471c-b5ad-6815adb78ca6
feature: Cache, Categories, Services
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# MDVA-30102: Redis キャッシュがいっぱいです

MDVA-30102 パッチは、Redis キャッシュがいっぱいになり、エラーが発生する問題を解決します。この問題により、製品リスト ページ（PLP）と製品詳細ページ（PDP）に問題が生じ、製品が見つからないなどの問題が発生します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.6 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 - 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Redis キャッシュがいっぱいで、割り当て済み `maxmemory` 不十分なようだ。 レイアウトキャッシュに TTL がなく、エビクションされませんでした。これにより、キャッシュが増加し、Redis の他のキーがエビクションされました。 その結果、すべての Redis メモリがレイアウトキャッシュに割り当てられました。

<u>前提条件</u>:

* Adobe Commerce 2.4 を使用し、100,000 個のシンプルな商品（商品の種類は関係ありません）と 50 個のカテゴリを持つ必要があります。
* Redis キャッシュは、次の手順に従って設定する必要があります。 [Adobe Commerce設定ガイド / Adobe Commerce ページとデフォルトキャッシュに Redis を使用する](https://devdocs.magento.com/guides/v2.4/config-guide/redis/redis-pg-cache.html#example-command) 開発者向けドキュメントを参照してください。

<u>再現手順</u>:

1. すべての PDP と PLP を参照します。 次を使用できます [OWASP ZAP](https://www.zaproxy.org/) サイトをクロールします。
1. Redis のメモリ使用状況を確認します。
1. また、現在の設定と使用中のメモリも確認します。 CLI で次のコマンドを実行します。 使用中のメモリ、maxmemory、エビクトキー、Redis のアップ時間を日数でチェックします。

```
redis-cli -p REDIS_PORT -h REDIS_HOST info | egrep --color "(role|used_memory_peak|maxmemory|evicted_keys|uptime_in_days)"
```

<u>期待される結果</u>:

Redis キャッシュは急速に増加してはいけません。

<u>実際の結果</u>:

Redis キャッシュは最大 5 GB まで増加します。 Redis のメモリは 8GB の上限があるため、100 万個の製品がある場合は、メモリが非常に早く不足します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
