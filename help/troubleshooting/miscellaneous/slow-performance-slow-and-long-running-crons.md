---
title: パフォーマンスが遅く、動作が遅く、長時間実行されるクローン
description: この記事では、フラットテーブルとインデクサーが有効になっていることが原因で発生する、サイトのパフォーマンスの問題と、実行が遅く停止したクローンを解決する方法について説明します。
exl-id: a78ca3c3-85b4-40a1-a693-4703dd3ef4b5
feature: Best Practices, Cache, Categories, Catalog Management
role: Developer
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# パフォーマンスが遅く、動作が遅く、長時間実行されるクローン

>[!WARNING]
>
>どのAdobe Commerce バージョンでも、一部の拡張機能はフラットテーブルでのみ機能するので、フラットテーブルを無効にした場合にリスクが生じます。 フラットカタログインデクサーを使用する拡張機能があることがわかっている場合は、それらの値を「」に設定する際に、その点を考慮する必要があります *不可* 」と入力します。

この記事では、サイトのパフォーマンスの問題を解決する方法と、によって発生する実行が遅くなったり停止したりする問題を解決する方法について説明します [フラットテーブルとインデクサー](https://docs.magento.com/m2/ce/user_guide/catalog/catalog-flat.html) が有効になっています。

影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.1.x 以降でのAdobe Commerce
* Adobe Commerce オンプレミス 2.1.x 以降
* Magento Open Source 2.1.x 以降

## 問題

フラットインデクサーは次の原因となる可能性があります。

* SQL 負荷が高く、サイトのパフォーマンスに問題がある。
* 長い間実行して立ち往生したクローン。

## 原因：

フラットなテーブルとインデクサーが有効になっています。

## 解決策 {#solution}

Adobe CommerceおよびMagento Open Source 2.1.x 以降では、フラットなカタログの使用はベストプラクティスではないので、お勧めしません。 この機能を継続的に使用すると、パフォーマンスの低下やその他のインデックス作成の問題が発生することが知られています。 フラット・カタログを無効にする手順は、次のとおりです。

1. 管理者で、に移動します。 **ストア** > **設定** > **設定**.
1. の下にある左側のパネル **カタログ** 、を選択 **カタログ**.
1. を展開します。 **ストアフロント** を選択し、次の手順を実行します。
   * を設定 **フラット カタログ カテゴリを使用** 対象： *不可*.
   * を設定 **フラットカタログ製品を使用** 対象： *不可*.
1. 完了したら、 **設定を保存**. プロンプトが表示されたら、キャッシュを更新します。
1. 実行によるキャッシュのフラッシュ `php bin/magento cache:flush`.

を変更できない場合 **フラット カタログ カテゴリを使用** および **フラットカタログ製品を使用** 対象： *不可* オプションはグレー表示されているので、でフラットインデクサーを無効にします。 `app/etc/config.php`:

1. 次のコマンドを実行して、すべてのインデクサーがスケジュールに従って更新に設定されていることを確認します。 `php bin/magento indexer:set-mode schedule`.
1. 編集 `app/etc/config.php` を使用して行を特定します `flat_catalog_product` および `flat_catalog_category`  – これらを 1 から 0 に変更して無効にします。
1. コマンドを実行します `php bin/magento app:config:import`
1. 次のコマンドを実行して、フラット・インデクサーが無効化されていることを確認します。 `php        bin/magento indexer:status`.
1. 実行によるキャッシュのフラッシュ `php bin/magento cache:flush`.

## 関連情報

[Cloud でスタックしたAdobe Commerce cron ジョブを手動でリセット](/help/how-to/general/reset-stuck-magento-cron-jobs-manually-on-cloud.md) サポートナレッジベースで。
