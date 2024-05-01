---
title: 「ACSD-51892：設定ファイルが複数回読み込まれるパフォーマンスの問題」
description: ACSD-51892 パッチを適用して、のデプロイメント中に設定ファイルが複数回読み込まれるAdobe Commerceのパフォーマンスの問題を修正してください。
feature: Observability
role: Admin
exl-id: 397343df-360f-43c4-bcef-be5f0da5aeef
source-git-commit: 97734799a39f41d0d6441379e21608fa5fcd1d4c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# ACSD-51892：設定ファイルが複数回読み込まれるパフォーマンスの問題

ACSD-51892 パッチは、 `app/etc/env.php` および `app/etc/config.php` ファイル：1 回のリクエスト内でデプロイメント設定値にアクセスするたびに生成されます。 ファイルの過度の読み取りは、システムに負担をかけ、全体的なパフォーマンスの低下につながります。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.33 がインストールされています。 パッチ ID は ACSD-51892 です。 この問題はAdobe Commerce 2.4.6-p2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定ファイルが複数回読み込まれるパフォーマンスの問題があります。

<u>再現手順</u>:

1. デプロイメントを実行するか、Adobe Commerce 2.4.6 以降にアップグレードします。
1. へのアクセスに関するファイルシステムログの確認 `app/etc/env.php` および `app/etc/config.php` の配置中にファイルが見つかりました。

<u>期待される結果</u>:

デプロイメントは通常の期間内に成功します。

<u>実際の結果</u>:

* サーバは、入力したコマンドに応答するのに苦労しています。 この結果、 *エラー 503 最初のバイトのタイムアウト* web サイトへのアクセス時。
* へのアクセス権を持つ複数のエントリがログファイルにあります `app/etc/env.php` および `app/etc/config.php` ファイル。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
