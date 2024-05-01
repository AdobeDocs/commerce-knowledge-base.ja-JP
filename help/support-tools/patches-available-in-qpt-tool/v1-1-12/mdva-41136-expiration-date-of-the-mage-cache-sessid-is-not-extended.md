---
title: '「MDVA-41136: mage-cache-sessid の有効期限が拡張されていません」'
description: MDVA-41136 パッチは、「mage-cache-sessid」 cookie の有効期限が延長されず、顧客のデータクリーンアップが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-41136。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 7673d084-1ed2-4f1d-8525-e665b971baf2
feature: Cache
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# MDVA-41136: mage-cache-sessid の有効期限が拡張されていません

MDVA-41136 パッチは、の有効期限が `mage-cache-sessid` cookie が拡張されないので、顧客データがクリーンアップされる。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-41136。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

の有効期限 `mage-cache-sessid` が拡張されないので、顧客データがクリーンアップされます。

<u>再現手順</u>:

1. Commerce Admin で、に移動します。 **ストア** > **設定** > **Web** > **デフォルトの Cookie 設定** > およびを設定 **Cookie の有効期間** 60 まで。
1. ストアフロントで顧客としてログインします。
1. に移動 **マイアカウント**.
1. 30 秒後にページをリロードします。

<u>期待される結果</u>:

ヘッダーに顧客の名前が表示されます。

<u>実際の結果</u>:

ヘッダーに顧客の名前がなく、 *デフォルトのウェルカムメッセージ* メッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
