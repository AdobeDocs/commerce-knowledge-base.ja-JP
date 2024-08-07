---
title: 「MDVA-38132：バックエンド URL がデフォルトの web サイト URL と異なる場合の無限リダイレクト」
description: MDVA-38132 パッチでは、バックエンド URL がデフォルトの Web サイト URL と異なる場合の無限リダイレクトの問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.25 がインストールされている場合に利用できます。 パッチ ID は MDVA-38132。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 122145d7-0961-47f8-8ab6-a15d62996e49
feature: Cache
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# MDVA-38132: バックエンド URL がデフォルトの Web サイト URL と異なる場合の無限リダイレクト

MDVA-38132 パッチでは、バックエンド URL がデフォルトの Web サイト URL と異なる場合の無限リダイレクトの問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.25 がインストールされている場合に使用できます。 パッチ ID は MDVA-38132。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**
Adobe Commerce（すべてのデプロイメント方法） 2.3.3-2.4.2-p1
>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Commerce管理パネルには、バックエンド URL がデフォルトの web サイト URL と異なる場合、無限のリダイレクトがあります。

<u> 前提条件 </u>:

* ベース URL はバックエンドとストアフロントの両方で使用されます。 ベース セキュア URL は使用されません。
* Web サーバーは、Adobe Commerceが 2 つの異なる URL からアクセスできるように設定されています。 URL1 は、Adobe Commerceのインストールに使用されます。

<u> 再現手順 </u>:

1. 管理パネル/**ストア**/**設定**/**Web** に移動します。
1. 元のベース URL はグローバル設定のままにします。 これは URL です 1。
1. メイン Web サイトの範囲に切り替えます。
1. ベース URL を別の URL に変更します（web サーバーを正しく設定するための前提条件を参照）。 これは URL2 です。
1. キャッシュをクリアします（必要に応じて、可能な場合）。
1. 管理パネルを開きます。

<u> 期待される結果 </u>:

管理パネルが正常に開かれ、移動できます。 メインの Web サイトのストアが正常に開かれ、ナビゲートできます。

<u> 実際の結果 </u>:

無限リダイレクトが発生します。 Adobe Commerceは URL1 から URL2 にリダイレクトし、前後に進みます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
