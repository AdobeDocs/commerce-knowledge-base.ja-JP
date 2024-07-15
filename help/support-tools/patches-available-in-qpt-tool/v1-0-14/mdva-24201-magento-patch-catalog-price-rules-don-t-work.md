---
title: 「MDVA-24201：カタログ価格ルールが機能しない」
description: MDVA-24201 パッチは、データベース内のアクティブなカタログ価格ルールがフロントエンドに適用されない問題を解決します。
exl-id: ae541c40-403a-46e9-a486-2a1e8991f05a
feature: Catalog Management, Categories, Marketing Tools, Orders, Price Rules
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# MDVA-24201: カタログ価格ルールが機能しない

MDVA-24201 パッチは、データベース内のアクティブなカタログ価格ルールがフロントエンドに適用されない問題を解決します。

このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.14 がインストールされている場合に使用できます。 この問題は、Adobe Commerce バージョン 2.3.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.3 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce on-premises 2.3.0 - 2.3.4-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 前提条件 </u>:

サンプルデータを含んだ新しいMagentoインスタンスをインストールします。

<u> 再現手順 </u>:

1. **管理パネル**/**マーケティング**/**カタログ価格ルール**/**新しいルールを追加** にログインし、次の設定を行います。
   1. **ルール名** を設定します。
   1. Set **Active** = *No.*
   1. **カテゴリ** = *4* の条件を設定します。 （例：バッグ）
   1. アクションを設定：
      1. 設定 **適用先**   **オリジナルのパーセンテージ**。
      1. **割引額** = *10* を設定します。
      1. 保存して、編集を続行します。
   1. 「**新しい更新をスケジュール**」をクリックします。
      * **ルール名** を設定します。
      * **アクティブ** = *はい* を設定します。
      * 保存します。
1. バックエンドに移動し、次を実行します。

   `php    bin/magento cron:run`

<u> 期待される結果 </u>:

カテゴリ 4 「バッグ」の製品の価格は、カタログ価格ルールで設定されていたので、期待どおりに元の価格の 10% を減らす必要があります。

<u> 実際の結果 </u>:

カタログ価格ルールがアクティブでも、価格変更は発生しません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
