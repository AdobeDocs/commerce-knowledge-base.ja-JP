---
title: 「MDVA-34012 パッチ：属性チェックボックスがエラーで変更される」
description: MDVA-34012 パッチを使用すると、エラーでスケジュールを更新した後に属性のチェックボックスが変更される問題を解決できます。
exl-id: 1a8f1bea-9b6a-4984-b9f0-b2b9ceb6688f
feature: Attributes
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# MDVA-34012 パッチ：属性チェックボックスがエラーで変更される

MDVA-34012 パッチを使用すると、エラーでスケジュールを更新した後に属性のチェックボックスが変更される問題を解決できます。

このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.17 がインストールされている場合に使用できます。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.5-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.3.1～2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. 管理者にログインし、**カタログ/製品** に移動します。
1. 簡単な製品を編集します。
1. ストア表示を特定のストア表示に変更する。
1. 属性に対して「**デフォルト値を使用**」チェックボックスを選択して製品を保存します（例：**製品を有効にする** 属性）。
1. 「**新規更新をスケジュール**」をクリックして、一部の変更をスケジュールします（特定の店舗表示の場合は「**価格** または **特別価格**）。
1. 変更が完了するまで待ちます。
1. 商品を確認してください。 チェックボックスをオフにし、特定のストア属性値を指定する必要があります。

<u> 期待される結果 </u>:

属性のチェックボックスは同じままで、スケジュールの更新後に期待どおりに変更されません。

<u> 実際の結果 </u>:

属性のチェックボックスは、スケジュールの更新後に変更されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
