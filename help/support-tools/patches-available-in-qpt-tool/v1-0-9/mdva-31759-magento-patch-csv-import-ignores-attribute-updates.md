---
title: 「MDVA-31759 パッチ：CSV の読み込みで属性の更新が無視される」
description: MDVA-31759 パッチでは、CSV の読み込みで*Dropdown*および*Text Area* タイプの追加の属性が無視される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.9 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 5426866c-893f-4abe-bfbc-6e7b30dd8dab
feature: Attributes, Data Import/Export
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# MDVA-31759 パッチ：CSV の読み込みは、属性の更新を無視します

MDVA-31759 パッチでは、CSV の読み込みで *Dropdown* タイプおよび *Text Area* タイプの追加の属性が無視される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.9 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

CSV の読み込みでは、*ドロップダウン* タイプや *テキスト領域* タイプの追加の属性が無視されます。

<u> 再現手順 </u>:

1. Commerce Admin にログインします。
1. 次の設定で製品属性を作成します。
   * **既定のラベル**: *G003*
   * **店舗所有者のカタログ入力タイプ**:*テキスト領域* または *ドロップダウン*
   * **属性コード**: *G003*
   * **範囲**: *グローバル*
1. 上記の属性をデフォルトの属性セットに追加します。
1. デフォルトの属性が設定された製品を作成し、新しい属性の値を指定します。
1. 製品を CSV に書き出します。
1. **additional\_attributes** 列の属性値を更新します。
1. 更新した CSV を読み込みます。

<u> 期待される結果 </u>:

G003 の属性値が更新されます。

<u> 実際の結果 </u>:

G003 属性値は更新されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
