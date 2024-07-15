---
title: 「MDVA-34189：ビジュアルマーチャンダイザーが長い MySQL クエリを実行する」
description: MDVA-34189 パッチを使用すると、管理者カテゴリページの読み込み時にAdobe Commerceで大規模なビジュアルマーチャンダイザークエリが実行される問題を解決できます。
exl-id: 94143d80-3240-4a18-890d-fb759ea9c30d
feature: Categories, Merchandising, Services
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# MDVA-34189：ビジュアルマーチャンダイザーが長い MySQL クエリを実行する

MDVA-34189 パッチを使用すると、管理者カテゴリページの読み込み時にAdobe Commerceで大規模なビジュアルマーチャンダイザークエリが実行される問題を解決できます。

このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.18 がインストールされている場合に使用できます。 パッチ ID は MDVA-34189。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.5-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.4-2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Web サイトでは、実稼動サーバー上で大規模な MySQL クエリを実行します。

<u> 再現手順 </u>:

1. ビジュアルマーチャンダイザーにアクセスするには、*管理者* サイドバーに移動し、**カタログ**/**カテゴリ** をクリックします。
1. 管理パネルで **カテゴリ** ページを読み込み（最初に読み込まれるルートカテゴリ）、実行されるクエリを確認します。

<u> 期待される結果 </u>:

管理者 **カテゴリ** ページは、低速のクエリを生成せずに読み込まれる必要がある。

<u> 実際の結果 </u>:

これは PHP の設定によって異なります。 このエラーの最も一般的な例は、**Categories** ページが開かず、エラー *Error 503 first byte timeout* が表示されることです。

または、Adobe Commerceがビジュアルマーチャンダイザーを読み込むと、低速の MySQL クエリが実行されます。 このクエリには、`ORDER BY FIELD(`e`.`entity_id`,  ...)` に挿入された多くの製品 ID が含まれています

`app/code/Magento/VisualMerchandiser/Model/Category/Products.php:: applyPositions` 内

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
