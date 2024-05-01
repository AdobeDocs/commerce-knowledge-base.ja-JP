---
title: 「MDVA-12304：ストアフロントで 503 エラーが発生し、cookie エラーが発生する」
description: この MDVA-12304 Adobe Commerce パッチは、店舗前面の 503 エラーを解決します。*Unable to send the cookie です。 Cookie の最大数を超えます。* ログのエラーメッセージ。 これは既知のAdobe Commerce 2.2.5 問題です。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.12 がインストールされている場合に利用できます。
exl-id: b4b1a2f7-f328-488f-86b8-576b908792fb
feature: Storefront
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# MDVA-12304：ストアフロントで 503 エラーが発生し、cookie エラーが発生する

この MDVA-12304 Adobe Commerce パッチは、次のような場合に、店舗前面での 503 エラーを解決します。 *Cookie を送信できません。 Cookie の最大数を超えます。* ログのエラーメッセージ。 これは既知のAdobe Commerce 2.2.5 問題です。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.12 がインストールされています。

## 影響を受ける製品とバージョン

* **Adobe Commerce バージョン用のパッチが作成されます。** Adobe Commerce オンプレミス 2.2.5。
* **Adobe Commerce バージョンとの互換性：** Adobe Commerce（すべてのデプロイメント方法） 2.x.x

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアの前面を移動すると、503 エラーが発生します。 が含まれる `var/log/exception.log` ファイル次のエラーメッセージがあります *Cookie を送信できません。 Cookie の最大数を超えます。*

この問題は、Adobe Commerceのデフォルト cookie 制限が 50 に設定されており、クライアントのブラウザーがこの制限に達すると、Commerceが例外をスローすることが原因で発生します。 パッチで提供されるソリューションでは、cookie の制限が 200 に増加されます。

<u>再現手順：</u>

顧客がログインして買い物かごを表示しようとすると、503 エラーはいつでも表示される可能性があります。

が含まれる `var/log/exception.log` ファイル次のエラーメッセージがあります *Cookie を送信できません。 Cookie の最大数を超えます。*

<u>実際の結果：</u> 顧客は買い物かごを確認したり、注文を完了したりできません。

<u>期待される結果：</u> 顧客は買い物かごを確認して、注文を完了できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。


## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
