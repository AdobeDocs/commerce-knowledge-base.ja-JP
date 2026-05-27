---
title: B2B 1.5.2 アップデート後のMagento_Company モジュールアップグレードのパフォーマンスの問題
description: この記事では、B2B 1.5.2のアップデート後にMagento_Company モジュールアップグレードで発生したパフォーマンスの問題に関するホットフィックスを提供します。company_structure テーブルの大規模なデータセットの処理時間が非常に長くなることに対処します。
feature: B2B, Upgrade
role: Admin, Developer
exl-id: b091d761-2e8a-4535-b461-ee9a46b5c2bc
source-git-commit: e0524b54ee0adae1caa809212e98dda3a33c1954
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# B2B 1.5.2 アップデート後のMagento_Company モジュールアップグレードのパフォーマンスの問題

この記事では、B2B 1.5.2の更新後にアップグレードされた`Magento_Company` モジュールのパフォーマンスに関する問題に関するホットフィックスを提供し、`company_structure` テーブルの大規模なデータセット（約100,000以上のレコード）の処理時間が非常に長くなることに対処します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-px + B2B 1.5.2
* Adobe Commerce（すべてのデプロイメント方法） 2.4.7-px + B2B 1.5.2
* Adobe Commerce（すべてのデプロイメント方法） 2.4.8 + B2B 1.5.2

## イシュー

B2B 1.5.2に更新した後に`Magento_Company` モジュールをアップグレードすると、`company_structure` テーブルで多数のレコード（～100,000以上）を処理する際に非常に長い時間がかかります。

<u>前提条件</u>:

* ACSD-65540_B2B_1.5.2.patchをインストールします。
* Adobe Commerce 2.4.6 - 2.4.8
* ACSD-65540 パッチが適用されたB2B バージョン 1.5.0、1.5.1、またはB2B バージョン 1.5.2

<u>複製する手順</u>:

1. 会社を親の会社に割り当てて、会社の階層を確立します。 詳しくは、Adobe Commerce B2B ガイドの[企業階層の管理](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/company-management/manage-company-hierarchy)を参照してください。
1. B2Bを1.5.2 バージョンにアップグレードします。

<u>期待される結果</u>:

アップグレードが正常に完了しました。

<u>実際の結果</u>:

`company_structure` テーブルに多数のレコードがある場合、`Magento_Company` モジュールのアップグレードを完了するのに時間がかかります。

## Solution

この問題を解決するには、次の手順を実行します。

1. B2B モジュールを1.5.2 バージョンに更新します。

   ```
   composer require magento/module-b2b:1.5.2 --no-update
   composer update magento/module-b2b
   ```

1. [ACSD-65540_B2B_1.5.2.patch](/help/troubleshooting/installation-and-upgrade/assets/ACSD-65540_B2B_1.5.2.zip)を適用します。

1. 添付の[ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patch](/help/troubleshooting/installation-and-upgrade/assets/ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patch.zip)を適用します。
1. パッチ適用後に`bin/magento setup:upgrade`を実行します。

### パッチの適用方法

ファイルを解凍し、手順については、サポートナレッジベースの[Adobe](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento)が提供するコンポーザーパッチの適用方法を参照してください。

### クラウドパッチを使用したパッチの適用

Adobe Commerce on Cloud マーチャントの場合は、次の手順に従います。

1. Cloud-patches モジュールのバージョンを1.1.5に更新して、MCLOUD-13605として配布されたACSD-65540_B2B_1.5.2.patchをインストールします。

   >[!NOTE]
   >
   >パッチが既にインストールされているかどうかを確認するには、以下を実行します。
   > `./vendor/bin/magento-patches -n status | grep MCLOUD-13605`

   ```
   composer require magento/magento-cloud-patches:1.1.5 --no-update
   composer update magento/magento-cloud-patches
   ```

1. ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patchを`m2-hotfixes` ディレクトリに追加します。
1. 変更をコミットしてプッシュし、再デプロイと`bin/magento setup:upgrade`を開始します。 手順については、Adobe Commerce on Cloud ガイドの「[&#x200B; パッチを適用](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/upgrade/apply-patches)」を参照してください。

## 関連トピックス

* [REGEXP_LIKE関数が欠落しているため、B2B 1.5.2へのアップグレードがSQL構文エラーで失敗する](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/sql-syntax-error-due-to-missing-regexp-like-function)
