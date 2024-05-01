---
title: 'MDVA-33970 パッチ：クレジット メモの通貨記号'
description: MDVA-33970 パッチを適用すると、クレジット メモにローカライズされた通貨ではなくドル記号（$）が表示される問題が解決されます。 これは、**Web サイト**スコープが**価格**属性に使用されている場合に発生します。
exl-id: 47a03067-86ef-4a55-8c21-921781062b53
feature: Orders, Returns
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# MDVA-33970 パッチ：クレジット メモの通貨記号

MDVA-33970 パッチを適用すると、クレジット メモにローカライズされた通貨ではなくドル記号（$）が表示される問題が解決されます。 これは、 **Web サイト** スコープは、 **価格** 属性。

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.15 がインストールされています。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.4 - 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>前提条件</u>:

この例では、次の設定が使用されます。

* 2 つの Web サイトが存在し、それぞれに **ストア** および **ストア表示**.
* この **デフォルトの設定** シンガポールドルを～とする **通貨** （**ストア/設定/一般/通貨の設定**）:
   * **基準通貨** = *ドル （シンガポール）*
   * **既定の表示通貨** = *ドル （シンガポール）*
   * **許可される通貨** = *ドル （シンガポール）*
* **Web サイト 1** 持つ **デフォルトの設定**.
* **Web サイト 2** マレーシアのリンギは～である **通貨**:
   * **基準通貨** = *マレーシア リンギ*
   * **既定の表示通貨** = *マレーシア リンギ*
   * **許可される通貨** = *マレーシア リンギ*
* に移動 **ストア /通貨記号**、および次のように設定します。
   * **MYR （マレーシア リンギ）** = *RM*
   * **SGD （シンガポールドル）** = *SGD* （**標準を使用** = *確認済み*）
* 一部 **製品** が存在する。

<u>再現手順</u>:

1. を作成 **順序** から **Web サイト 2** （追加の設定を避けるために、デフォルトとして設定できます）。
1. ログイン先 **Admin**.
1. 新しく作成した注文を開きます。
1. を確認します。 **通貨記号** = *RM*.
1. を作成 **請求書**.
1. を確認します。 **通貨記号** = *RM* 請求書に記載されています。
1. を作成 **クレジット メモ**.
1. を確認します。 **通貨記号**  ** ** = *RM* が含まれる **クレジット メモ**.
1. を開きます **クレジットメモ** タブ **順序**.
1. を確認します **通貨記号** グリッドの
1. 開く **売上 > クレジット・メモ**.
1. を確認します **通貨記号** グリッドの

<u>期待される結果</u>:

正しくローカライズされた通貨記号が、期待どおりに使用されます。

<u>実際の結果</u>:

ドル記号（$）は、管理設定で設定されていなくても使用されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
