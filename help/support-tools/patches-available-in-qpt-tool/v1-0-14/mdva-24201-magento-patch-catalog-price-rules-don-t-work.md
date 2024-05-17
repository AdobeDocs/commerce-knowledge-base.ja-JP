---
title: 「MDVA-24201：カタログ価格ルールが機能しない」
description: MDVA-24201 パッチは、データベース内のアクティブなカタログ価格ルールがフロントエンドに適用されない問題を解決します。
exl-id: ae541c40-403a-46e9-a486-2a1e8991f05a
feature: Catalog Management, Categories, Marketing Tools, Orders, Price Rules
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# MDVA-24201: カタログ価格ルールが機能しない

MDVA-24201 パッチは、データベース内のアクティブなカタログ価格ルールがフロントエンドに適用されない問題を解決します。

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.14 がインストールされています。 この問題は、Adobe Commerce バージョン 2.3.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー上のAdobe Commerce 2.3.3

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.3.4-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>前提条件</u>:

サンプルデータを含んだ新しいMagentoインスタンスをインストールします。

<u>再現手順</u>:

1. へのログイン **管理パネル** > **Marketing** > **カタログ価格ルール** > **新規ルールの追加**&#x200B;で、次の設定を行います。
   1. を **ルール名**.
   1. を設定 **アクティブ** = *いいえ。*
   1. 条件を設定： **カテゴリ** = *4*. （例：バッグ）
   1. アクションを設定：
      1. を設定 **適用先**   **オリジナルの割合**.
      1. を設定 **割引額** = *10*.
      1. 保存して、編集を続行します。
   1. クリックする **新しい更新をスケジュール**:
      * を **ルール名**.
      * を設定 **アクティブ** = *はい*.
      * 保存します。
1. バックエンドに移動し、次を実行します。

   `php    bin/magento cron:run`

<u>期待される結果</u>:

カテゴリ 4 「バッグ」の製品の価格は、カタログ価格ルールで設定されていたので、期待どおりに元の価格の 10% を減らす必要があります。

<u>実際の結果</u>:

カタログ価格ルールがアクティブでも、価格変更は発生しません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
