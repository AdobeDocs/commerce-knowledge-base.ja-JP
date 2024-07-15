---
title: 「MDVA-32759 パッチ：共有カタログ削除階層価格」
description: MDVA-32759 パッチは、共有カタログが既存の階層価格を削除する問題を解決します。
exl-id: c6192d2f-cd25-483e-ba69-01ca62996faf
feature: B2B, Catalog Management
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# MDVA-32759 パッチ：共有カタログ削除層の価格

MDVA-32759 パッチは、共有カタログが既存の階層価格を削除する問題を解決します。

このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.15 がインストールされている場合に使用できます。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 前提条件 </u>:

**B2B 機能** を有効にした B2B を使用してAdobe Commerceをインストールします。

<u> 再現手順 </u>:

1. **ストア/設定/B2B 機能/会社を有効にする** および **共有カタログ** に移動します。
1. `bin/magento cron:run` を実行します。
1. シンプルな製品を作成し、**詳細価格** をクリックして、**カタログと階層価格** を追加して保存します。
1. **カタログ/共有カタログ/価格と構造を設定** に移動し、「**設定**」をクリックし、そのドロップダウンメニューからすべてのオプションを選択解除して保存します。
1. `bin/magento cron:run` を実行します。
1. 上記で作成した製品を開き、詳細価格を確認します。

<u> 期待される結果 </u>:

期待どおりに、パブリック共有カタログからすべての製品を削除した後は、階層価格を製品から削除しないでください。

<u> 実際の結果 </u>:

階層価格は、公開共有カタログからすべての製品を削除した後に削除されます。


## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
