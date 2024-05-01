---
title: 「MDVA-37082：グループ化された製品の在庫ステータスの誤った部分インデックス」
description: MDVA-37082 Magentoパッチは、グループ化された商品の在庫ステータスの部分的なインデックスがカスタム在庫に対して間違っている場合の問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.25 がインストールされている場合に利用できます。 パッチ ID は MDVA-37082。 この問題はMagento 2.4.4 で修正される予定であることに注意してください。
exl-id: 1c0abc99-bd24-4848-87a3-227a63655cb7
feature: Cache, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# MDVA-37082：グループ化された製品の在庫状態のインデックスが正しくありません

MDVA-37082 Magentoパッチは、グループ化された商品の在庫ステータスの部分的なインデックスがカスタム在庫に対して間違っている場合の問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.25 がインストールされています。 パッチ ID は MDVA-37082。 この問題はMagento 2.4.4 で修正される予定であることに注意してください。


## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**
Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0-2.4.2-p1
>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

グループ化された製品の子製品のインデックスを増分すると、子が共有されたときに、他のグループ化された間違った製品が誤ってインデックス化される可能性があります。

<u>再現手順</u>:

* メイン web サイトの新しい在庫とソースを作成します。
* 数量 10、15 および 0 の 3 つの単純な製品を作成します。
* 2 つのグループ化された製品を作成し、数量 10 の最初の単純製品を一方に、他の 2 つの単純製品を他方に割り当てます。
* グループ化された両方の製品が、在庫としてフロントエンドからアクセスできることを確認します。
* 数量 0 の単純な製品を、最初にグループ化された製品のアップセル製品に割り当てます。
* フルページのキャッシュをクリーンアップし、フロントエンドから 2 番目のグループ化製品を確認します。
* 完全な再インデックスを実行します。
* フロントエンドから 2 番目にグループ化された製品を確認します。
* 最初のグループ化製品を保存します。
* フルページキャッシュをクリーンアップし、フロントエンドから 2 番目にグループ化された製品を確認します。

<u>期待される結果</u>:

グループ化された別の製品をアップセルで保存した後、グループ化された製品の在庫が切れていない。 この問題は、完全に再インデックスすると解決されます。

<u>実際の結果</u>:

2 番目のグループ化された製品は、1 番目のグループ化された製品を保存すると在庫切れになります。

## パッチの適用

個々のパッチを適用するには、Adobe Commerceのデプロイメント方法に応じて、開発者向けドキュメントへの次のリンクを使用します。

* Adobe Commerce オンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md).
* [Quality Patches Tool を使用して、Magentoの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md).

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
