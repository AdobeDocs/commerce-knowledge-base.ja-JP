---
title: 「MDVA-23426 Magentoパッチ：Outlook から添付ファイルとして送信されたメール」
description: MDVA-23426 Magentoパッチは、メールが MS Outlook からMagentoによって添付ファイルとして送信される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.13 がインストールされている場合に利用できます。 この問題はMagento 2.3.5 で修正されました。
exl-id: 0b4c3e33-76c5-48b0-b1a8-a967cea11b98
feature: Communications
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# MDVA-23426 Magento パッチ：Outlook から添付ファイルとして送信されたメール

MDVA-23426 Magentoパッチは、メールが MS Outlook からMagentoによって添付ファイルとして送信される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.13 がインストールされている場合に使用できます。 この問題はMagento 2.3.5 で修正されました。

## 影響を受ける製品とバージョン

**Magentoバージョン用のパッチが作成されます。** Magento Commerce Cloud 2.3.3。

**Magentoーバージョンとの互換性：** Magento CommerceおよびMagento Commerce Cloud 2.3.3 ～ 2.3.4-p2。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

メールは空白の本文で受信され、コンテンツは添付ファイルとして含まれます。

<u> 前提条件：</u> Outlook/Exchange はクライアントとサーバーの組み合わせとして使用されています。

<u> 再現手順：</u> 1. 注文を送信すると、注文通知または出荷通知が送信されます。2.メールが受信されます。

<u> 実際の結果：</u> メールは、空白の本文で表示され、コンテンツは、ATT\* ラベル付きのメール添付ファイルとして含まれます。 <u> 期待される結果：</u>

メールは添付ファイルなしで受信され、メールの本文にはコンテンツが含まれています。

## パッチの適用

QPT パッチを適用する手順については、Magentoに応じて次のリンクを使用してください。

* Magento Commerce: DevDocs [Quality Patches Tool を使用してパッチを適用します ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)。
* Magento Commerce Cloud: DevDocs[ アップグレードとパッチ/パッチを適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで適用する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool でパッチのMagentoの問題を確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
