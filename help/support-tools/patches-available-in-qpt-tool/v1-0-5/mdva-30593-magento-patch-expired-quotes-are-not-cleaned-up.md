---
title: 「MDVA-30593 パッチ：期限切れの引用符がクリーンアップされない」
description: MDVA-30593 パッチは、**Quote Lifetime**設定に従って期限切れになった引用符がクリーンアップされない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.5 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.3.4 で修正されました。
exl-id: 5ee91546-a5cb-4282-bdfc-c9bb3438af50
feature: Cache, Quotes
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# MDVA-30593 パッチ：期限切れの引用符はクリーンアップされない

MDVA-30593 パッチは、に従って有効期限が切れた引用符が付く問題を解決します。 **見積もりの有効期間** 設定は、クリーンアップされません。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.5 がインストールされています。 この問題はAdobe Commerce 2.3.4 で修正されました。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.3.x

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

引用符、に従って期限切れ **見積もりの有効期間** 設定は、クリーンアップされません。

<u>再現手順：</u>

1. Commerce Admin で、に移動します。 **ストア** > **設定** > **売上** > **チェックアウト** > **ショッピングカート**.
1. を設定 **見積もりの有効期間（日数）** = *1*
1. 設定を保存し、キャッシュをクリアします。
1. 顧客としてログインします。
1. 商品を買い物かごに追加します。
1. 1 日後、買い物かごに戻ります。

<u>期待される結果：</u>

古い価格が無効になったため、見積もりがクリアされ、商品が買い物かごから削除されます。

<u>実際の結果：</u>

商品はまだカートに入っています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
