---
title: 「MDVA-31590:MySQL 非同期キューを使用して一括で属性を更新できない」
description: MDVA-31590 パッチを適用すると、ユーザーが MySQL 非同期キューを使用して属性を一括で更新できない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.3 がインストールされている場合に利用できます。 パッチ ID は MDVA-31590。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 57db28dd-a739-4a77-927d-6339af4fa4a6
feature: Attributes, Services
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# MDVA-31590: MySQL 非同期キューを使用して属性を一括更新できない

MDVA-31590 パッチを適用すると、ユーザーが MySQL 非同期キューを使用して属性を一括で更新できない問題が解決されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.3 がインストールされています。 パッチ ID は MDVA-31590。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0-2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーは、MySQL 非同期を使用して属性を一括で更新できません。

<u>再現手順</u>:

1. バックエンドの商品グリッドで、一括アクションを実行して、いくつかの商品の属性値を更新します。
   * 製品を確認して選択 **属性を更新** 「アクション」ドロップダウンから選択します。
1. 必要な属性の値を設定し、製品を web サイトに割り当てて保存します。
1. ページがリロードされると、次のようなメッセージが表示されます。
   *タスク「選択した N 個の製品の属性を更新」:1 個の項目に対して更新がスケジュールされました。*
1. 数秒待ってから、バックエンドページをリロードします。

<u>期待される結果</u>:

1. ページに、次のような成功した更新メッセージが表示されます。 *1 個の項目が正常に更新されました。*
1. 関連製品の属性値が更新されます。
1. データベースでは、新しいレコードは両方に作成されます `magento_bulk` テーブルと `magento_operation` テーブル（一括に関連する操作）。
1. に新しいレコードが作成されます `queue_message` テーブル （キューに関連） `product_action_attribute.update` および/または `product_action_attribute.website.update`）に設定します。
1. `queue_message_status` テーブルには、ステータス「4」のレコードがあります。
1. にはエラーはありません `system.log`.

<u>実際の結果</u>:

1. ページには、引き続き次のようなメッセージが表示されます。
   *タスク「選択した N 個の製品の属性を更新」:1 個の項目に対して更新がスケジュールされました。*
1. 製品の属性値が更新されます。
1. 新しいレコードが次の場所に作成されます。 `message_bulk` テーブルに、関連するレコードがありません `magento_operation` テーブル。
1. 新しいレコードはに作成されます。 `queue_message` および `queue_message_status` テーブル。
1. `queue_message_status` テーブルには、エラーステータスのレコードがあります（ステータス値「6」）。
1. `system.log` 次のようなエラーが含まれます。
   *main.CRITICAL: メッセージが拒否されました：SQLSTATE[23000]：整合性制約違反：1048 列「operation_key」を null にすることはできません。クエリは次のとおりです：INSERT INTO {{magento_operation}} ({{id}}, {{bulk_uuid}}, {{topic_name}}, {{serialized_data}}, {{result_serialized_data}}, {{status}}, {{error_code}}, {{result_message}}, {{operation_key}}）値（?、?、?、?、?、?、?、?、?、? [][]*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
