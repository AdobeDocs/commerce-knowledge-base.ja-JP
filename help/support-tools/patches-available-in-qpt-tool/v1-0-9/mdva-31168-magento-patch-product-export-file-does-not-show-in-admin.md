---
title: 「MDVA-31168 パッチ：製品の書き出しファイルが管理者に表示されない」
description: MDVA-31168 パッチを適用すると、製品の書き出し CSV ファイルが書き出し可能な CSV ファイルのリストに表示されない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.10 がインストールされている場合に利用できます。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。
exl-id: 780a926b-2aea-47c2-8f95-907cc779bfa4
feature: Admin Workspace, Categories, Data Import/Export, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# MDVA-31168 パッチ：製品の書き出しファイルが管理者に表示されない

MDVA-31168 パッチを適用すると、製品の書き出し CSV ファイルが書き出し可能な CSV ファイルのリストに表示されない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.10 がインストールされている場合に使用できます。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Adobe Commerce オンプレミス 2.3.5-p2.

**Adobe Commerce バージョンとの互換性：** クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.3.0～2.4.1。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 前提条件 </u>:

サンプルデータを使用してAdobe Commerceをインストールします。

<u> 再現手順：</u>

1. ダウンロード可能な製品を作成し、**Bags** カテゴリに割り当てます。
1. すべての製品の書き出しを開始します。
1. CLI から次のコマンドを実行します。    ```php    bin/magento queue:consumers:start exportProcessor --single-thread --max-messages=10000    ```

<u> 期待される結果：</u>

すべての製品を含んだ製品の書き出し CSV ファイルは、期待どおりに Admin のファイルリストに表示されます。

<u> 実績：</u>

ヘッダーのみを含むファイルはサーバーの `/var` フォルダーで生成されますが、すべての製品を含む製品の書き出し CSV ファイルは Admin のリストには表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
