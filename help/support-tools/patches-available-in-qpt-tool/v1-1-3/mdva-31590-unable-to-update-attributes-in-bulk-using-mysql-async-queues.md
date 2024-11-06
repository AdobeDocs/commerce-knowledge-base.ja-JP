---
title: 「MDVA-31590:MySQL 非同期キューを使用して一括で属性を更新できない」
description: MDVA-31590 パッチを適用すると、ユーザーが MySQL 非同期キューを使用して属性を一括で更新できない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.3 がインストールされている場合に利用できます。 パッチ ID は MDVA-31590。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 57db28dd-a739-4a77-927d-6339af4fa4a6
feature: Attributes, Services
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# MDVA-31590: MySQL 非同期キューを使用して属性を一括更新できない

MDVA-31590 パッチを適用すると、ユーザーが MySQL 非同期キューを使用して属性を一括で更新できない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.3 がインストールされている場合に使用できます。 パッチ ID は MDVA-31590。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0-2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーは、MySQL 非同期を使用して属性を一括で更新できません。

<u> 再現手順 </u>:

1. バックエンドの商品グリッドで、一括アクションを実行して、いくつかの商品の属性値を更新します。
   * 製品を確認し、アクション ドロップダウンから **属性を更新** を選択します。
1. 必要な属性の値を設定し、製品を web サイトに割り当てて保存します。
1. ページがリロードされると、次のようなメッセージが表示されます。
   *タスク「選択した N 個の製品の属性を更新」:1 個の項目が更新にスケジュールされています。*
1. 数秒待ってから、バックエンドページをリロードします。

<u> 期待される結果 </u>:

1. ページに、「*1 個の項目が正常に更新されました。*」のような更新メッセージが表示されます。
1. 関連製品の属性値が更新されます。
1. DB では、新しいレコードは `magento_bulk` のテーブルと `magento_operation` のテーブルの両方に作成されます（一括に関連する操作）。
1. 新しいレコードが `queue_message` テーブルに作成されます（キュー `product_action_attribute.update` や `product_action_attribute.website.update` に関連）。
1. テ `queue_message_status` ブルには、ステータス「4」のレコードがあります。
1. `system.log` にエラーはありません。

<u> 実際の結果 </u>:

1. ページには、引き続き次のようなメッセージが表示されます。
   *タスク「選択した N 個の製品の属性を更新」:1 個の項目が更新にスケジュールされています。*
1. 製品の属性値が更新されます。
1. テーブルに新しいレコード `message_bulk` 作成されますが、テーブルに関連するレコードはあり `magento_operation` せん。
1. 新しいレコードが `queue_message` テーブルと `queue_message_status` テーブルに作成されます。
1. テ `queue_message_status` ブルには、エラーステータスを含むレコードがあります（ステータス値「6」）。
1. `system.log` 次のようなエラーが含まれています。
   *main.CRITICAL: メッセージが拒否されました：SQLSTATE[23000]：整合性制約違反：1048 カラム &#39;operation_key&#39;は null にできません、クエリは：INSERT INTO {{magento_operation}} ({{id}}, {{bulk_uuid}}, {{topic_name}}, {{serialized_data}}, {{result_serialized_data}}, {{status}}, {{error_code}}, {{result_message}}, {{operation_key}}）値（?、?、?、?、?、?、?、?、?、?） [][]*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
