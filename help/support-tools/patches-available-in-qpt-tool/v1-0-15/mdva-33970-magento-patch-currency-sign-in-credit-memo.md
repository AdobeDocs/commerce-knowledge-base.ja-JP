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

MDVA-33970 パッチを適用すると、クレジット メモにローカライズされた通貨ではなくドル記号（$）が表示される問題が解決されます。 これは、**Web サイト** スコープが **価格** 属性に使用されている場合に発生します。

このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.15 がインストールされている場合に使用できます。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce on-premises 2.3.4 - 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 前提条件 </u>:

この例では、次の設定が使用されます。

* 2 つの Web サイトが存在します。それぞれに **ストア** と **ストア表示** があります。
* **デフォルト設定** では、シンガポールドルは **通貨** です（**ストア/設定/一般/通貨設定**）。
   * **基準通貨** = *シンガポールドル*
   * **デフォルト表示通貨** = *シンガポールドル*
   * **使用可能な通貨** = *シンガポールドル*
* **Web サイト 1** には **デフォルト設定** があります。
* **Website 2** は、マレーシアのリンギを **通貨** としています。
   * **基準通貨** = *マレーシア リンギ*
   * **デフォルトの表示通貨** = *マレーシア リンギ*
   * **許可されている通貨** = *マレーシア リンギ*
* **ストア/通貨記号** に移動し、次を設定します。
   * **MYR （マレーシア リンギ）** = *RM*
   * **SGD （シンガポールドル）** = *SGD* （**標準を使用** = *オン*）
* 一部の **Product** が存在します。

<u> 再現手順 </u>:

1. **Web サイト 2** から **注文** を作成します（追加設定を避けるために、デフォルトとして設定できます）。
1. **Admin** にログインします。
1. 新しく作成した注文を開きます。
1. **通貨記号** = *RM* を確認します。
1. **請求書** を作成します。
1. 請求書の **通貨記号** = *RM* を確認します。
1. **クレジットメモ** を作成します。
1. **クレジット メモ** の通貨記号 ****** = *RM* であることを確認し** す。
1. **注文** の **クレジットメモ** タブを開きます。
1. グリッドの **通貨記号** を確認します。
1. **営業/クレジット・メモ** を開きます。
1. グリッドの **通貨記号** を確認します。

<u> 期待される結果 </u>:

正しくローカライズされた通貨記号が、期待どおりに使用されます。

<u> 実際の結果 </u>:

ドル記号（$）は、管理設定で設定されていなくても使用されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
