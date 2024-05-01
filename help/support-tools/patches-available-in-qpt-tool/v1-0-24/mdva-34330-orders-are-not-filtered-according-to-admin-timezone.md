---
title: 「MDVA-34330：管理タイムゾーンに従ってフィルタリングされていない注文」
description: MDVA-34330 パッチは、注文が管理者のタイムゾーンに従ってフィルタリングされない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.24 がインストールされている場合に利用できます。 パッチ ID は MDVA-34330。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: cb369ee3-60b0-4317-a448-0c4ed64f2816
feature: Admin Workspace, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# MDVA-34330：管理タイムゾーンに従ってフィルターされていない注文

MDVA-34330 パッチは、注文が管理者のタイムゾーンに従ってフィルタリングされない問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.24 がインストールされています。 パッチ ID は MDVA-34330。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメントタイプ） 2.3.1 ～ 2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者のタイムゾーンに従ってフィルタリングされていない注文。

<u>再現手順</u>:

1. に移動 **ストア** > 設定 > **設定** > **一般** を設定して、 **Timezone** 対象： *東部標準時（アメリカ/ニューヨーク）*
1. 00:00 UTC の後に新しい注文を行う
1. に移動 **売上** > **注文件数** および今日の日付でフィルタリング


<u>期待される結果</u>:

今日 00:00 UTC の後に配置された注文は、フィルタリングされた結果に表示されます。

<u>実際の結果</u>:

フィルタリングされた結果に順序がありません。

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md).
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md).

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
