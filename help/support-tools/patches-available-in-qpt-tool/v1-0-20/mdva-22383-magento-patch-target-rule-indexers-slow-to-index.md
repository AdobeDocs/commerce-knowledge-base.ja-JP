---
title: 「MDVA-22383：インデックス作成が遅いターゲットルールインデクサー」
description: MDVA-22383 パッチを適用すると、製品/ターゲットルールおよびターゲットルール/製品インデクサーのインデックス再作成に時間がかかりすぎる問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.20 がインストールされている場合に利用できます。 パッチ ID は MDVA-22383。 この問題はAdobe Commerce 2.3.5 で修正されました。
exl-id: fbf28983-5883-4769-90bd-1c97c2b2e2b8
source-git-commit: 975f5b5c95ad488128a5dbb3488b8d54f7b73b59
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# MDVA-22383: ターゲット ルール インデクサーのインデックス作成が遅い

MDVA-22383 パッチを適用すると、製品/ターゲットルールおよびターゲットルール/製品インデクサーのインデックス再作成に時間がかかりすぎる問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.20 がインストールされている場合に使用できます。 パッチ ID は MDVA-22383。 この問題はAdobe Commerce 2.3.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce on-premises 2.3.0-2.3.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品/ターゲットルールおよびターゲットルール/製品インデクサーのインデックス再作成に時間がかかりすぎます。

<u> 前提条件：</u> この問題は製品が多数ある場合に発生します。

<u> 再現手順：</u>

1. 条件に一致する製品を含むターゲットルールを作成します。条件は、コレクションにさらに製品を追加する必要があり、（カテゴリや属性セットではなく）属性を持つ必要があります。
1. 次のコマンドを実行します。

   ```bash
       bin/magento indexer:reindex targetrule_product_rule
   ```

<u> 実際の結果：</u>

インデックス再作成が停止し、製品の保存が停止する。

<u> 期待される結果：</u>

インデックス再作成が正常に完了しました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
