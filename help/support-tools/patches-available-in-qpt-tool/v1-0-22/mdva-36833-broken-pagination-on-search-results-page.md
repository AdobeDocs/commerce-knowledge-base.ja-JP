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

MDVA-36833 パッチでは、共有カタログが有効になっていて、一部の製品が共有カタログから除外されている場合にページネーションが機能しない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.22 がインストールされている場合に使用できます。 パッチ ID は MDVA-36833。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用にパッチが作成されます。** Adobe Commerce（すべてのデプロイメント方法） 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

共有カタログから一部の製品を除外すると、検索結果のページネーションが壊れる。

<u> 再現手順：</u>

1. Shared Catalog を有効にします。
1. **カタログ**/**共有カタログ** に移動し、すべての製品を割り当ててデフォルトの共有カタログを設定します。
1. ストアフロントを読み込んで、「ジャケット」を検索します。
1. 最初のページにリストされている製品に注意してください。 12 個の製品があるはずです。
1. 最初のページの 11 個の SKU を書き留めます。 バックエンドに移動し、デフォルトの共有カタログを読み込みます。
1. デフォルトの共有カタログから、以前にメモした SKU の割り当てを解除します。
1. ストアフロントに移動し、「ジャケット」を検索します。
1. 検索結果の最初のページを確認します。

<u> 実際の結果：</u>

最初のページには 1 つの製品があり、残りの製品は 2 番目のページで利用できます。

<u> 期待される結果：</u>

最初のページには 12 個の製品が必要です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。


## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
