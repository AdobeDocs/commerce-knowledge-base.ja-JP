---
title: 「MDVA-26639：新しい注文確認メールテンプレートに注文項目がありません」
description: MDVA-26639 パッチは、新しい注文が作成され、確認メールテンプレートに注文項目が見つからない場合の問題を修正します。
exl-id: 5d9716ab-6e57-47b0-8b38-ca98a98101e8
feature: Communications, Marketing Tools, Native Luma Frontend Development, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# MDVA-26639：新しい注文確認メール テンプレートに注文項目がありません

MDVA-26639 パッチは、新しい注文が作成され、確認メールテンプレートに注文項目が見つからない場合の問題を修正します。

このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.20 がインストールされています。 パッチ ID は MDVA-26639。 この問題はAdobe Commerce 2.3.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー上のAdobe Commerce 2.3.3-p1

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.3-p1-2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. に移動 **ストア** > **設定** > **売上** > **販売メール** > **新規注文確認** を選択して、 **テンプレート：新規集荷注文**.
1. に移動 **売上** > **注文：注文を選択します**&#x200B;に移動します。 **情報**&#x200B;を選択し、 **メールを送信**.

<u>期待される結果</u>:

注文項目は、期待どおりに顧客注文メールに表示されます。

<u>実際の結果</u>:

顧客注文メールに注文項目がありません。 新しいテンプレートを作成し、テンプレートとして「新規注文」または「新規注文」（Luma）を選択した場合も同じことが当てはまります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
