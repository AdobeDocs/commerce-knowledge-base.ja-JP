---
title: 「MDVA-35312：空のGraphQL リクエストで 500 エラーがスローされる（200 OK ではない）」
description: MDVA-35312 パッチでは、空のGraphQL リクエストがエラー応答コード 500 をスローする問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.18 がインストールされている場合に利用できます。 パッチ ID は MDVA-35312。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 345fdbd4-8a43-4aab-a318-72792c8a7a78
feature: GraphQL
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# MDVA-35312：空のGraphQL リクエストで 500 エラーがスローされる（200 OK ではない）

MDVA-35312 パッチでは、空のGraphQL リクエストがエラー応答コード 500 をスローする問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.18 がインストールされています。 パッチ ID は MDVA-35312。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Magentoバージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.2 上のAdobe Commerce

**Magentoバージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.1-p1-2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

空のGraphQL リクエストが、200 コードではなくエラー応答コード 500 をスローする。

<u>再現手順</u>:

GraphQL リクエストを送信する。例：

```curl
curl -i -X OPTIONS http://inv.test/graphql
```

<u>期待される結果</u>:

応答： *200 OK*.

<u>実際の結果</u>:

応答： *HTTP/1.1 500 内部サーバーエラー*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
