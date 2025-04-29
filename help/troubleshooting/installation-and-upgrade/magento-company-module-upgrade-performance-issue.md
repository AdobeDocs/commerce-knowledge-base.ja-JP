---
title: B2B 1.5.2 の更新後のMagento_Company モジュールのアップグレードにおけるパフォーマンスの問題
description: この記事では、B2B 1.5.2 の更新後にMagento_Company モジュールをアップグレードする際のパフォーマンスの問題に関するホットフィックスを提供し、company_structure テーブル内の大規模なデータセットの処理時間が過度に長くなる問題に対処します。
feature: B2B, Upgrade
role: Admin, Developer
source-git-commit: d06f0045b4c4c1615bd3abec963eb17fdee93860
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# B2B 1.5.2 の更新後のMagento_Company モジュールのアップグレードにおけるパフォーマンスの問題

この記事では、B2B 1.5.2 へのアップデート後に `Magento_Company` モジュールをアップグレードする際のパフォーマンスの問題に関するホットフィックスを提供し、`company_structure` テーブル内の大規模なデータセット（100,000 件以上のレコード）の処理時間が非常に長くなる問題に対処します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-px + B2B 1.5.2
* Adobe Commerce（すべてのデプロイメント方法） 2.4.7-px + B2B 1.5.2
* Adobe Commerce（すべてのデプロイメント方法） 2.4.8 + B2B 1.5.2

## 問題

B2B 1.5.2 に更新した後に `Magento_Company` モジュールをアップグレードすると、`company_structure` テーブルに大量のレコード（～100,000 以上）が処理される際に非常に長い時間がかかる。

<u> 前提条件 </u>:

* ACSD-65540_B2B_1.5.2.patch がインストールされている必要があります。
* Adobe Commerce 2.4.6 - 2.4.8
* ACSD-65540 パッチが適用された B2B バージョン 1.5.0、1.5.1、または B2B 1.5.2

<u> 再現手順 </u>:

1. 会社を親会社に割り当てて、会社の階層を確立します。 詳しくは、Adobe Commerce B2B ガイドの [ 会社階層の管理 ](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/company-management/manage-company-hierarchy) を参照してください。
1. B2B を 1.5.2 バージョンにアップグレードします。

<u> 期待される結果 </u>:

アップグレードが正常に完了しました。

<u> 実際の結果 </u>:

`company_structure` テーブルに多数のレコードがある場合、`Magento_Company` モジュールのアップグレードの完了には時間がかかります。

## 解決策

この問題を解決するには、次の手順を実行します。

1. B2B モジュールを 1.5.2 バージョンに更新します。

   ```
   composer require magento/module-b2b:1.5.2 --no-update
   composer update magento/module-b2b
   ```

1. [ACSD-65540_B2B_1.5.2.patch](/help/troubleshooting/installation-and-upgrade/assets/ACSD-65540_B2B_1.5.2.zip) を適用します。

1. 添付の [ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patch](/help/troubleshooting/installation-and-upgrade/assets/ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patch.zip) を適用します。
1. パッチを適用した後、`bin/magento setup:upgrade` を実行します。

### パッチの適用方法

ファイルを解凍し、サポートナレッジベースの [Adobeが提供する Composer パッチの適用方法 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento) を参照してください。

### クラウドパッチを使用したパッチの適用

Cloud マーチャント上のAdobe Commerceの場合は、次の手順に従います。

1. MCLOUD-13605 として配布されている ACSD-65540_B2B_1.5.2.patch をインストールするには、cloud-patches モジュールのバージョンを 1.1.5 に更新します。

   >[!NOTE]
   >
   >パッチが既にインストールされているかどうかを確認するには、次の手順を実行します。
   > `./vendor/bin/magento-patches -n status | grep MCLOUD-13605`

   ```
   composer require magento/magento-cloud-patches:1.1.5 --no-update
   composer update magento/magento-cloud-patches
   ```

1. ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patch を `m2-hotfixes` ディレクトリに追加します。
1. 変更をコミットしてプッシュし、再デプロイと `bin/magento setup:upgrade` プロイメントを開始します。 手順については、Cloud 上のAdobe Commerce ガイドの [ パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/upgrade/apply-patches) を参照してください。

## 関連資料

* [REGEXP_LIKE 関数がないため、SQL 構文エラーで B2B 1.5.2 へのアップグレードが失敗します ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/sql-syntax-error-due-to-missing-regexp-like-function)
