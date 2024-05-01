---
title: 「ACSD-50478：バックアップグリッドおよびデータベースロールバックコマンドでのロールバックアクションの JS の問題」
description: ACSD-50478 パッチを適用して、DB ダンプにトリガーと*delimiter* SQL コマンドが含まれている場合のバックアップ グリッドおよびデータベース ロールバック コマンドでのロールバック アクションの JS の問題を修正してください。
exl-id: 8b516705-29be-462e-b3ec-3a339b6e8006
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# ACSD-50478：バックアップグリッドおよびデータベースロールバックコマンドでのロールバックアクションの JS の問題

ACSD-50478 パッチは、DB ダンプにトリガーおよびが含まれている場合のバックアップ グリッドおよびデータベース ロールバック コマンドのロールバック アクションの JS の問題を修正します。 *区切り文字* SQL コマンド。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされています。 パッチ ID は ACSD-50478 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.4-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

DB ダンプにトリガーおよびが含まれる場合の Backups グリッドの rollback アクションと database rollback コマンドの JS の問題 *区切り文字* SQL コマンド。

<u>再現手順</u>:

1. インデクサーをに設定 [!UICONTROL Update on Schedule] トリガーがデータベースに作成されるように設定します。
1. コマンドラインからバックアップ機能を有効にします。

   `bin/magento config:set system/backup/functionality_enabled 1`

1. に移動 **システム** > **ツール** > **バックアップ** DB バックアップを生成します。
1. ブラウザーコンソールを開くと、次のエラーが表示されます。

   ```
   Uncaught SyntaxError: Unexpected token '&' (at (index):606:32)
   
   function eventListener8jtGaqtgG2 () {
   
           return backup.rollback(&#039;db&#039;, &#039;1678391644&#039;);
   ```

1. コマンドラインから DB をインポートします。

   `bin/magento setup:rollback --db-file="<filename>"`

1. 次のエラーが表示されます。

   ```
   Syntax error or access violation: 1064 You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'delimiter' at line 1, query was: delimiter ;;
   ```

<u>期待される結果</u>:

データベースの復元は、管理者とコマンドラインの両方から正常に行われます。

<u>実際の結果</u>:

手順 4 と手順 6 で示したエラーが表示されました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
