---
title: 「MDVA-34886:「weight」属性を使用しても検索結果が表示されない」
description: MDVA-34886 パッチは、weight 属性が検索可能として設定されている場合に検索が結果を返す問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.16 がインストールされている場合に利用できます。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: e6f33772-0167-4a54-9d62-0ab89edb5d1d
feature: Attributes, Cache, Search
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# MDVA-34886:「weight」属性を使用しても検索結果が表示されない

MDVA-34886 パッチは、weight 属性が検索可能として設定されている場合に検索が結果を返す問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.16 がインストールされています。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.2 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

weight 属性が検索可能として設定されている場合、検索結果が返されます。

<u>再現手順</u>:

1. Elasticsearchを設定します。
1. に移動します。 **Admin** > **ストア** > **属性** > **製品**. を編集する **ウェイト** 属性とその属性の設定 **検索可能** = *はい*.
1. 属性を保存し、設定キャッシュをクリアします。
1. フロントエンドで、テキスト値を検索します（例： *バッグ*）に設定します。
1. 検索が結果を返さないことを確認します。
1. 例外ログには、次のようなエラーメッセージが含まれます。

```php
{"type":"number_format_exception","reason":"For input string: \"bag\""}
```

<u>期待される結果</u>:

weight 属性が期待どおりに検索可能として設定されている場合でも、検索結果が返されます。

<u>実際の結果</u>:

weight 属性が検索可能として設定されている場合、検索結果は返されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
