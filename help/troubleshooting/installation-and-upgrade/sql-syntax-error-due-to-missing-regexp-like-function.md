---
title: REGEXP_LIKE関数が欠落しているため、B2B 1.5.2へのアップグレードがSQL構文エラーで失敗する
description: この記事では、company_structure テーブルを更新しようとしたときにREGEXP_LIKE関数が見つからなかったためにSQL構文エラーが発生する問題の修正プログラムを提供します。
feature: B2B, Upgrade
role: Admin, Developer
exl-id: c5fe316c-99e3-482e-80b5-25aaae371230
source-git-commit: 1dcd003bd9b08741c0fba464f5520797cfaeccbb
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# REGEXP_LIKE関数が欠落しているため、B2B 1.5.2へのアップグレードがSQL構文エラーで失敗する

>[!INFO]
>
>B2B 1.5.2への更新後に`Magento_Company` モジュールをアップグレードする際にパフォーマンスの問題が発生した場合は、添付の[ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patch](assets/ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patch.zip)を適用します。
>
>詳しくは、Adobe Commerce ナレッジベースの「[B2B 1.5.2 アップデート後のMagento_Company モジュールのアップグレードにおけるパフォーマンスの問題](/help/troubleshooting/installation-and-upgrade/magento-company-module-upgrade-performance-issue.md)」を参照してください。

この記事では、`REGEXP_LIKE` テーブルを更新しようとしたときに欠落している`company_structure`関数が原因で発生するSQL構文エラーのホットフィックスを提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方式） 2.4.6-px + B2B 1.5.2 （[!DNL MariaDB] 10.6を使用）
* Adobe Commerce（すべてのデプロイメント方式） 2.4.7-px + B2B 1.5.2 （[!DNL MariaDB] 10.6を使用）

## イシュー

B2B バージョン 1.5.2へのアップグレードは、`REGEXP_LIKE` テーブルの更新時に`company_structure`関数が欠落しているため、SQL構文エラーで失敗します。

<u>前提条件</u>:

* MariaDB 10.6
* Adobe Commerce 2.4.6倍または2.4.7倍
* B2B バージョン 1.5.0または1.5.1

<u>複製する手順</u>:

1. 会社を親の会社に割り当てて、会社の階層を確立します。 詳しくは、Adobe Commerce B2B ガイドの[企業階層の管理](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/company-management/manage-company-hierarchy)を参照してください。
1. B2Bを1.5.2 バージョンにアップグレードします。

<u>期待される結果</u>:

アップグレードが正常に完了しました。

<u>実際の結果</u>:

`bin/magento setup:upgrade`は次のエラーで失敗します：

```
Unable to apply data patch Magento\Company\Setup\Patch\Data\SetCompanyForStructure for module Magento_Company. Original exception message: SQLSTATE[42000]: Syntax error or access violation: 1305 FUNCTION REGEXP_LIKE does not exist, query was: UPDATE `company_structure` SET `company_id` = ? WHERE (REGEXP_LIKE(path, '^123(/.+)?$'))
```

## Solution

この問題を解決するには、次の手順を実行します。

1. B2B モジュールを1.5.2 バージョンに更新します。

   ```
   composer require magento/module-b2b:1.5.2 --no-update
   composer update magento/module-b2b
   ```

1. 添付の[ACSD-65540_B2B_1.5.2.zip](assets/ACSD-65540_B2B_1.5.2.zip) パッチを適用します。 手順については、サポートナレッジベースの[Adobeが提供するコンポーザーパッチの適用方法を参照してください。](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/how-to-apply-a-composer-patch-provided-by-magento)
1. `bin/magento setup:upgrade`を実行します。

### クラウドパッチを使用したパッチの適用

Adobe Commerce on Cloud インフラストラクチャの場合は、次の手順に従います。

1. `cloud-patches` モジュールのバージョンを1.1.5に更新：

   ```
   composer require magento/magento-cloud-patches:1.1.5 --no-update
   composer update magento/magento-cloud-patches
   ```

1. 変更をコミットしてプッシュし、再デプロイを開始します。 手順については、Adobe Commerce on Cloud ガイドの「[ パッチを適用](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/upgrade/apply-patches)」を参照してください。
