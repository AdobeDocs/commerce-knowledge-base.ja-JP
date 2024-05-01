---
title: 「MDVA-35064:API を使用して作成された設定可能ファイルに対して、URL の書き換えが生成されない」
description: MDVA-35064 パッチでは、API を使用して作成された製品の「すべてのストアビュー」に対して URL の書き換えが生成されない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.17 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 0898c5b3-d361-4bcb-af3a-7f76ac8a23e1
feature: REST, Categories, Configuration
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# MDVA-35064: API を使用して作成された構成に対して、URL の書き換えが生成されない

MDVA-35064 パッチでは、API を使用して作成された製品の「すべてのストアビュー」に対して URL の書き換えが生成されない問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.17 がインストールされています。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.3-2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

API を使用して設定可能な製品が作成された場合、URL の書き換えは生成されません。

<u>再現手順</u>:

1. 新しい web サイト、ストア、ストア表示を作成します。
1. 新しいカテゴリを作成します。
1. 新しい製品を作成し、新しく作成したカテゴリに割り当てます。
1. 製品をメインの web サイトと新しい web サイトに割り当てます。
1. URL テーブルを調べ、各 web サイト上の各ストアの製品、カテゴリ、製品のエントリが含まれていることを確認します。
1. 2 番目の web サイトの製品を削除します。

<u>期待される結果</u>:

URL テーブルには、最初の web サイトのストアに対してのみ、製品、カテゴリ、製品のエントリが含まれます。

<u>実際の結果</u>:

URL テーブルには、すべての web サイト上のすべてのストアの URL 書き換えが含まれます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
