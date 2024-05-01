---
title: 「MDVA-36833：検索結果ページのページネーションが壊れる」
description: MDVA-36833 パッチでは、共有カタログが有効になっていて、一部の製品が共有カタログから除外されている場合にページネーションが機能しない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.22 がインストールされている場合に利用できます。 パッチ ID は MDVA-36833。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 7105c4ed-48d9-4d4c-bf12-5914bbad62da
feature: Catalog Management, Search
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# MDVA-36833：検索結果ページのページネーションが壊れている

MDVA-36833 パッチでは、共有カタログが有効になっていて、一部の製品が共有カタログから除外されている場合にページネーションが機能しない問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.22 がインストールされています。 パッチ ID は MDVA-36833。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Adobe Commerce（すべてのデプロイメント方法） 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

共有カタログから一部の製品を除外すると、検索結果のページネーションが壊れる。

<u>再現手順：</u>

1. Shared Catalog を有効にします。
1. に移動 **カタログ** > **共有カタログ** デフォルトの共有カタログを設定するには、すべての製品を割り当てます。
1. ストアフロントを読み込んで、「ジャケット」を検索します。
1. 最初のページにリストされている製品に注意してください。 12 個の製品があるはずです。
1. 最初のページの 11 個の SKU を書き留めます。 バックエンドに移動し、デフォルトの共有カタログを読み込みます。
1. デフォルトの共有カタログから、以前にメモした SKU の割り当てを解除します。
1. ストアフロントに移動し、「ジャケット」を検索します。
1. 検索結果の最初のページを確認します。

<u>実際の結果：</u>

最初のページには 1 つの製品があり、残りの製品は 2 番目のページで利用できます。

<u>期待される結果：</u>

最初のページには 12 個の製品が必要です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。


## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
