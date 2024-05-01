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

このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.18 がインストールされています。 パッチ ID は MDVA-34189。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.4-2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Web サイトでは、実稼動サーバー上で大規模な MySQL クエリを実行します。

<u>再現手順</u>:

1. ビジュアルマーチャンダイザーにアクセスするには、 *Admin* サイドバー、クリック **カタログ** > **カテゴリ**.
1. を読み込みます **カテゴリ** 管理パネルのページ（最初に読み込まれるルートカテゴリ）で、実行されるクエリを確認します。

<u>期待される結果</u>:

管理者 **カテゴリ** 低速のクエリを生成せずにページを読み込む必要がある。

<u>実際の結果</u>:

これは PHP の設定によって異なります。 このエラーの最も一般的な例は、 **カテゴリ** エラーでページが開かない *エラー 503 最初のバイトのタイムアウト* が表示されます。

または、Adobe Commerceがビジュアルマーチャンダイザーを読み込むと、低速の MySQL クエリが実行されます。 このクエリには、に挿入された多くの製品 ID が含まれています `ORDER BY FIELD(`e`.`entity_id`,  ...)`

。対象： `app/code/Magento/VisualMerchandiser/Model/Category/Products.php:: applyPositions`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
