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

この MDVA-12304 Adobe Commerce パッチは、ストアフロントで 503 エラーを解決します。*Cookie を送信できません。 Cookie の最大数を超えます。ログに* のエラーメッセージがあります。 これは既知のAdobe Commerce 2.2.5 問題です。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.12 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

* **Adobe Commerce バージョン用のパッチが作成されます。** Adobe Commerce オンプレミス 2.2.5。
* **Adobe Commerce バージョンとの互換性：** Adobe Commerce（すべてのデプロイメント方法） 2.x.x

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアの前面を移動すると、503 エラーが発生します。 `var/log/exception.log` ファイルに「Cookie を送信できません *というエラーメッセージが表示されます。 Cookie の最大数を超えます。*

この問題は、Adobe Commerceのデフォルト cookie 制限が 50 に設定されており、クライアントのブラウザーがこの制限に達すると、Commerceが例外をスローすることが原因で発生します。 パッチで提供されるソリューションでは、cookie の制限が 200 に増加されます。

<u> 再現手順：</u>

顧客がログインして買い物かごを表示しようとすると、503 エラーはいつでも表示される可能性があります。

`var/log/exception.log` ファイルに「Cookie を送信できません *というエラーメッセージが表示されます。 Cookie の最大数を超えます。*

<u> 実績結果：</u> お客様は、カートの確認や注文の完了はできません。

<u> 期待される結果：</u> 顧客は買い物かごを確認して、注文を完了できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。


## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
