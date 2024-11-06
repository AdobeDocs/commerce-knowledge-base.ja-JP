---
title: パフォーマンスが遅く、動作が遅く、長時間実行されるクローン
description: この記事では、フラットテーブルとインデクサーが有効になっていることが原因で発生する、サイトのパフォーマンスの問題と、実行が遅く停止したクローンを解決する方法について説明します。
exl-id: a78ca3c3-85b4-40a1-a693-4703dd3ef4b5
feature: Best Practices, Cache, Categories, Catalog Management
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# パフォーマンスが遅く、動作が遅く、長時間実行されるクローン

>[!WARNING]
>
>どのAdobe Commerce バージョンでも、一部の拡張機能はフラットテーブルでのみ機能するので、フラットテーブルを無効にした場合にリスクが生じます。 フラットカタログインデクサーを使用する拡張機能があることがわかっている場合は、それらの値を「*いいえ*」に設定する際に、その点を考慮する必要があります。

この記事では、[ フラットテーブルとインデクサー ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/catalog-flat) が有効になっていることが原因で発生する、サイトのパフォーマンスの問題と、実行が遅く停止した cron を解決する方法について説明します。

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

1. 管理者で、**ストア**/**設定**/**設定** に移動します。
1. 左側の **カタログ** の下にあるパネルで、「**カタログ**」を選択します。
1. **Storefront** セクションを展開し、次の操作を実行します。
   * **フラット カタログ カテゴリを使用** を *いいえ* に設定します。
   * **フラットカタログ製品を使用** を *いいえ* に設定します。
1. 完了したら、「**設定を保存**」をクリックします。 プロンプトが表示されたら、キャッシュを更新します。
1. `php bin/magento cache:flush` を実行してキャッシュをフラッシュします。

オプションがグレー表示されているため、「**フラット カタログ カテゴリを使用**」および「**フラット カタログ製品を使用**」を *いいえ* に変更できない場合は、`app/etc/config.php` でフラット インデクサーを無効にします。

1. このコマンドを実行して、すべてのインデクサーがスケジュールに従って更新に設定されていることを確認します：`php bin/magento indexer:set-mode schedule`。
1. `app/etc/config.php` を編集して、`flat_catalog_product` と `flat_catalog_category` がある行を見つけます。無効にするには、1 から 0 に変更します。
1. コマンド `php bin/magento app:config:import` を実行します。
1. 次のコマンドを実行して、フラット インデクサーが無効になっていることを確認します：`php        bin/magento indexer:status`。
1. `php bin/magento cache:flush` を実行してキャッシュをフラッシュします。

## 関連情報

サポートナレッジベースの [ スタックしたAdobe Commerce cron ジョブを Cloud で手動でリセット ](/help/how-to/general/reset-stuck-magento-cron-jobs-manually-on-cloud.md) します。
