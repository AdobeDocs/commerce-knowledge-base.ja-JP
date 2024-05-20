---
title: 'MDVA-28651: B2B – 引用符の読み込みに時間がかかる'
description: MDVA-28651 パッチを適用すると、引用符の読み込みによってパフォーマンスに関するいくつかの問題が発生する問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） v.1.0.9 がインストールされている場合に利用できます。 この問題はAdobe Commerce バージョン 2.4.2 で修正される予定だったことに注意してください。
exl-id: 2d0bfbba-cdf3-4f9e-a900-ce42909fac8e
feature: B2B, Quotes
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# MDVA-28651: B2B – 引用符の読み込みに時間がかかる

MDVA-28651 パッチを適用すると、引用符の読み込みによってパフォーマンスに関するいくつかの問題が発生する問題が解決されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) v.1.0.9 がインストールされます。 この問題はAdobe Commerce バージョン 2.4.2 で修正される予定だったことに注意してください。

## 影響を受ける製品とバージョン

* このパッチは、クラウドインフラストラクチャー 2.3.4 上のAdobe Commerce用に設計されました。
* また、このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0-2.3.5-p1、2.4.0 および 2.4.1 のAdobe Commerce バージョンとも互換性があります。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

お客様の見積リスト・ページのパフォーマンスに関する問題：

* 引用リストの二重読み込み：最初はページ全体、2 番目は Ajax リクエスト。
* プラグインから各引用符を読み込むループ。
* 見積もりがスナップショットに変換された際の見積もり品目のダブルロード。

<u>再現手順</u>

1. お客様に 40 以上の見積りを割り当てる。
1. ログインして、 **自分の見積もり** ページ。

<u>実際の結果</u>

のコンテンツを完全に読み込むための応答時間 **自分の見積もり** ページ（ページの読み込み+ グリッドに表示されるデータ）は約 45 秒です。

<u>期待される結果</u>

のコンテンツを完全に読み込むための応答時間 **自分の見積もり** ページは 45 秒未満である必要があります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
