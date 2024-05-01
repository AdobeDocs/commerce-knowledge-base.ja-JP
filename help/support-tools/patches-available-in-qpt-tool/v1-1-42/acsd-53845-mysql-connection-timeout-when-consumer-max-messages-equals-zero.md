---
title: 「ACSD-53845:consumer max_messages = 0 の場合の MySQL 接続タイムアウトの問題」
description: コンシューマー「max_messages = 0」の場合に MySQL 接続がタイムアウトするAdobe Commerceの問題を修正するために、ACSD-53845 パッチを適用してください。
feature: REST, Configuration
role: Admin, Developer
exl-id: 68f862ed-5401-41e9-a6cc-cef44ebc1915
source-git-commit: 6fa7182a807147a00ad750966cd839ec18ffe0c7
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# ACSD-53845：コンシューマー時の MySQL 接続タイムアウトの問題 `max_messages = 0`

ACSD-53845 パッチは、コンシューマーが MySQL 接続をタイムアウトにする問題を修正します `max_messages = 0`. このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.42 がインストールされています。 パッチ ID は ACSD-53845 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

コンシューマーが起動すると MySQL 接続がタイムアウトする `max_messages = 0`.

ただし、トランザクションを開始すると、データベースへの接続が復元されます。

<u>再現手順</u>:

1. を使用して製品を一括更新するリクエストを送信 `async/bulk/V1/products` REST API エンドポイント。
1. でのステータスの確認 `magento_operation` テーブル。

<u>期待される結果</u>:

製品が更新されます。

<u>実際の結果</u>:

1. ログにエラーが記録されます。

   ```
   report.CRITICAL: Message has been rejected: SQLSTATE[HY000]: General error: 2006 MySQL server has gone away [] []
   ```

1. *ステータス* この操作は残っています *4* が含まれる `magento_operation` テーブル。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
