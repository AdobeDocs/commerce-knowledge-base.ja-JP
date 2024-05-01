---
title: 「MDVA-32776：注文を行っても在庫ステータスが更新されない」
description: MDVA-32776 パッチは、注文が行われても出荷されなかった場合に在庫ステータスが更新されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.6 がインストールされている場合に利用できます。 パッチ ID は MDVA-32776。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 10e9458f-562a-480b-b813-104a93db4308
feature: Orders
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# MDVA-32776：発注時に在庫ステータスが更新されない

MDVA-32776 パッチは、注文が行われても出荷されなかった場合に在庫ステータスが更新されない問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.1.6 がインストールされています。 パッチ ID は MDVA-32776。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.0

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文したが出荷されていない場合、在庫ステータスは更新されません。

<u>前提条件</u>:

1. 在庫モジュールがインストールされています。
1. 在庫切れ商品の表示はに設定されています。 *はい*.

   設定するには、に移動します。 **ストア** > **設定** > **カタログ** > **在庫** > **在庫切れ商品を表示** = *はい*.

<u>再現手順</u>:

1. 数量=11 と 22 の 2 つの単純な製品を作成します。
1. 手順 1 で作成した簡単な製品を使用して、グループ化された製品を作成します。
1. 製品数量の 1 つを 11 に設定し、他の単純な製品を在庫切れにすることで、グループ化された製品を買い物かごに追加します。
1. チェックアウトを完了し、注文を行います。

<u>期待される結果</u>:

グループ化された製品の表示 `out-of-stock` 関連付けられたシンプルな製品が在庫切れになった場合のラベル。

<u>実際の結果</u>:

1. 数量= 11 のシンプル製品は、在庫切れを示しています。
1. グループ化された製品に *在庫切れ* 数量= 11 の商品のメッセージ。 ただし、この商品を買い物かごに追加すると、次のメリットがあります *在庫切れ* エラー。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
