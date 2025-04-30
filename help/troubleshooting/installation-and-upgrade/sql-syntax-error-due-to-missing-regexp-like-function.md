---
title: REGEXP_LIKE 関数がないため、B2B 1.5.2 へのアップグレードが SQL 構文エラーで失敗します
description: この記事では、company_structure テーブルを更新しようとしたときに、REGEXP_LIKE 関数が見つからないことが原因で SQL 構文エラーが発生する問題のホットフィックスを提供します。
feature: B2B, Upgrade
role: Admin, Developer
exl-id: c5fe316c-99e3-482e-80b5-25aaae371230
source-git-commit: 04e17dfdf143e233eb2767064c1328990c899eda
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# REGEXP_LIKE 関数がないため、B2B 1.5.2 へのアップグレードが SQL 構文エラーで失敗します

>[!INFO]
>
>B2B 1.5.2 に更新した後、`Magento_Company` モジュールをアップグレードする際にパフォーマンスの問題が発生した場合は、添付の [ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patch](assets/ACSD-65540_B2B_1.5.2_DEPENDENT_ACSD-65684_B2B_1.5.2.patch.zip) を適用します。
>
>詳しくは、Adobe Commerce ナレッジベースの [B2B 1.5.2 アップデート後のMagento_Company モジュールのアップグレードにおけるパフォーマンスの問題 ](/help/troubleshooting/installation-and-upgrade/magento-company-module-upgrade-performance-issue.md) を参照してください。

この記事では、`company_structure` テーブルを更新しようとしたときに `REGEXP_LIKE` 関数が見つからなかったことが原因で発生する SQL 構文エラーのホットフィックスを示します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-px + B2B 1.5.2 （[!DNL MariaDB] 10.6 を使用）
* Adobe Commerce（すべてのデプロイメント方法） 2.4.7-px + B2B 1.5.2 （[!DNL MariaDB] 10.6 を使用）

## 問題

`company_structure` テーブルの更新時に `REGEXP_LIKE` 関数が見つからないため、B2B バージョン 1.5.2 へのアップグレードが失敗し、SQL 構文エラーが発生します。

<u> 前提条件 </u>:

* MariaDB 10.6
* Adobe Commerce 2.4.6x または 2.4.7x
* B2B バージョン 1.5.0 または 1.5.1

<u> 再現手順 </u>:

1. 会社を親会社に割り当てて、会社の階層を確立します。 詳しくは、Adobe Commerce B2B ガイドの [ 会社階層の管理 ](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/company-management/manage-company-hierarchy) を参照してください。
1. B2B を 1.5.2 バージョンにアップグレードします。

<u> 期待される結果 </u>:

アップグレードが正常に完了しました。

<u> 実際の結果 </u>:

`bin/magento setup:upgrade` が次のエラーで失敗します：

```
Unable to apply data patch Magento\Company\Setup\Patch\Data\SetCompanyForStructure for module Magento_Company. Original exception message: SQLSTATE[42000]: Syntax error or access violation: 1305 FUNCTION REGEXP_LIKE does not exist, query was: UPDATE `company_structure` SET `company_id` = ? WHERE (REGEXP_LIKE(path, '^123(/.+)?$'))
```

## 解決策

この問題を解決するには、次の手順を実行します。

1. B2B モジュールを 1.5.2 バージョンに更新します。

   ```
   composer require magento/module-b2b:1.5.2 --no-update
   composer update magento/module-b2b
   ```

1. 添付の [ACSD-65540_B2B_1.5.2.zip](assets/ACSD-65540_B2B_1.5.2.zip) パッチを適用します。 手順については、サポートナレッジベースの [Adobeが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。
1. `bin/magento setup:upgrade` を実行します。

### クラウドパッチを使用したパッチの適用

クラウドインフラストラクチャー上のAdobe Commerceの場合は、次の手順に従います。

1. `cloud-patches` モジュールのバージョンを 1.1.5 に更新します。

   ```
   composer require magento/magento-cloud-patches:1.1.5 --no-update
   composer update magento/magento-cloud-patches
   ```

1. 変更をコミットしプッシュして、再デプロイを開始します。 手順については、Cloud 上のAdobe Commerce ガイドの [ パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/upgrade/apply-patches) を参照してください。
