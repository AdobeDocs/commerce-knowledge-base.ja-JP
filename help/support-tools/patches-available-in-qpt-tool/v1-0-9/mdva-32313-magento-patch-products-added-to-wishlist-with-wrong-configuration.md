---
title: 「MDVA-32313 パッチ：間違った設定でウィッシュリストに追加された製品」
description: MDVA-32313 パッチは、設定可能な製品がウィッシュリストに追加されたときに間違った設定が割り当てられるので、ウィッシュリストに正しく追加できない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.10 がインストールされている場合に利用できます。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。
exl-id: e7ac5ef5-1389-4108-b2bc-73d43eb3e7ca
feature: Configuration, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# MDVA-32313 パッチ：間違った設定でウィッシュリストに追加された製品

MDVA-32313 パッチは、設定可能な製品がウィッシュリストに追加されたときに間違った設定が割り当てられるので、ウィッシュリストに正しく追加できない問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.10 がインストールされています。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.3.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.3.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. 顧客を作成します。
1. 顧客アカウントにログインします。
1. に移動します。 **製品リスト** ページ。
1. 設定可能な製品の選択（例： *configurable\_1* ）を選択し、の色とサイズのオプションを選択します。 **製品リスト** ページ （**製品ページは開かないでください。**）に設定します。
1. 別の設定可能な製品のウィッシュリストアイコンをクリックします（例： *設定可能\_2*）を選択します。

<u>期待される結果</u>:

この *設定可能\_2* 製品は、オプションを選択せずに、期待どおりにウィッシュリストに追加されます。

<u>実際の結果</u>:

この *設定可能\_2* 製品が、からの設定でウィッシュリストに追加されました *configurable\_1* 製品。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
