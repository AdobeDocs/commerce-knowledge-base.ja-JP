---
title: 「MDVA-28763:REST API を使用した製品画像の管理に関する問題」
description: MDVA-28763 パッチは、REST API を使用したメディアギャラリーの管理に関連する複数の問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.5 がインストールされている場合に利用できます。 この問題は、今後のAdobe Commerce バージョンで修正される予定です。
exl-id: 736fbfa8-b6a3-413c-a220-fd772d87ed04
feature: REST, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# MDVA-28763:REST API を使用した製品画像の管理に関する問題

MDVA-28763 パッチは、REST API を使用したメディアギャラリーの管理に関連する複数の問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.5 がインストールされている場合に使用できます。 この問題は、今後のAdobe Commerce バージョンで修正される予定です（[ 問題 ](#issues) の問題の説明を参照してください）。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce オンプレミス 2.3.2 - 2.3.3.x
* クラウドインフラストラクチャー上のAdobe Commerce 2.3.2 - 2.3.3.x

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題 {#issues}

MDVA-28763 パッチには、メディアギャラリーに関連する次の問題に対する修正が含まれています。

* REST API を使用してYouTube ビデオを更新する場合（`PUT rest/V1/products/ {SKU}`、Adobe Commerceではビデオのサムネールが表示されますが、「再生」ボタンをクリックしてもビデオプレーヤーは読み込まれません。 Adobe Commerce 2.3.6 で修正予定です。
* `PUT /V1/products/:sku/media/:entryId` の呼び出しにより、既存のエントリが置き換わるのではなく、新しいエントリが作成されます。 Adobe Commerce 2.3.5 で修正されました。
* 製品が複数のストア表示に割り当てられている場合の製品画像削除の問題。 Adobe Commerce 2.3.4 で修正されました。
* 複数の web サイトを持つマーチャントは、画像と画像の役割の継承を維持しながら、REST を使用して製品を作成および更新できるようになりました。 以前は、マーチャントが REST を使用して商品を作成および更新し、ストア表示のために商品を更新した場合、デフォルトの画像の役割がそのストア表示のために読み込まれて保存されていました。 その結果、ストア表示の画像の役割は、更新後、デフォルトの範囲から継承されなくなります。 Adobe Commerce 2.3.6 で修正予定です。
* メディア属性（画像、サムネールなど） 削除された画像を参照するストアビューの値が自動的にクリーンアップされない。 Adobe Commerce 2.4.2 で修正予定です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
