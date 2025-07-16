---
title: APSB25-08 セキュリティパッチ後の一括非同期 web エンドポイントの実行時間が短縮されました
description: この記事では、APSB25-08 セキュリティパッチを適用した後、1000 以上のエントリに対する POST rest/all/async/bulk/V1/products リクエストの実行時間が大幅に長くなる問題のホットフィックスを提供します。
feature: Security, Cache, REST, Products, Customers
role: Admin, Developer
exl-id: 784a48cb-1ef1-432b-b09f-ebcbb9bebf01
source-git-commit: f0c2e20e0bd6dab713be59c1c686ee2948445bd4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# APSB25-08 セキュリティパッチ後のすべての一括非同期 web エンドポイントの実行時間が短縮されました

この記事では、1,000 以上のエントリを持つ `POST rest/all/async/bulk/V1/products` など、APSB25-08 セキュリティパッチを適用した後に実行時間が大幅に長くなる、すべての一括非同期 web エンドポイントのホットフィックスを提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4、2.4.4-p1、2.4.4-p2、2.4.4-p3、2.4.4-p4、2.4.4-p5、2.4.4-p6、2.4.4-p7、2.4.4-p8、2.4.4-p9、2.4.4-p10、2.4.4-p11、2.4.4-p11、2.4.4.4-p12

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5、2.4.5-p1、2.4.5-p2、2.4.5-p3、2.4.5-p4、2.4.5-p5、2.4.5-p6、2.4.5-p7、2.4.5-p8、2.4.5-p9、2.4.5-p10、2.4.5-p11

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6、2.4.6-p1、2.4.6-p2、2.4.6-p3、2.4.6-p4、2.4.6-p5、2.4.6-p6、2.4.6-p7、2.4.6-p8、2.4.6-p9

* Adobe Commerce（すべてのデプロイメント方法） 2.4.7、2.4.7-p1、2.4.7-p2、2.4.7-p3、2.4.7-p4

* Adobe Commerce（すべてのデプロイメント方法） 2.4.8

## 問題

APSB25-08 セキュリティパッチを適用した後、1,000 件以上のエントリを含む `POST rest/all/async/bulk/V1/products` リクエストの実行に大幅に時間がかかります。

<u> 再現手順 </u>:

1. 1000 件以上のエントリ（名前、SKU、説明で十分）を含んだ `POST rest/all/async/bulk/V1/products` リクエストを行います。
1. リクエストにかかる時間を書き留めます。
1. APSB25-08 セキュリティパッチを適用し、生成されたデータとキャッシュを `se:di:co` を使用してクリーンアップします。
1. `bin/magento c:f` を実行します。
1. ストアフロントに移動して、キャッシュと生成されたファイルが適切に配置されていることを確認します。
1. 手順 1 からのリクエストを繰り返します。
1. リクエストにかかる時間が長くなっていることに注意してください。
1. APSB25-08 セキュリティパッチを削除し、キャッシュをフラッシュして、コードを再生成し、手順 1 のリクエストを繰り返して、実行時間が通常に戻ったことを確認します。 （オプション）

<u> 期待される結果 </u>:

セキュリティパッチを適用した後、`async/bulk` リクエストの実行時間が大幅に長くなりました。

<u> 実際の結果 </u>:

セキュリティパッチを適用した後、`async/bulk` リクエストの実行時間が大幅に長くなることはありませんが、ある程度の時間延長が予想されます。

## 解決策

この問題を解決するには、[AC-14078-2-4x-composer-patch.zip](assets/AC-14078-2-4x-composer-patch.zip) を適用します。

## パッチの適用方法

ファイルを解凍し、サポートナレッジベースの [Adobeが提供する Composer パッチの適用方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html?lang=ja) を参照してください。

## 関連資料

* [Adobe Commerceでセキュリティアップデートが利用可能 – APSB25-08](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27149)
