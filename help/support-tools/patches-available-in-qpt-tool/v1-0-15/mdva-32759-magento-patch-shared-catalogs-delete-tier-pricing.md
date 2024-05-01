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

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.15 がインストールされています。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>前提条件</u>:

B2B と共にAdobe Commerceをインストール **B2B の機能** 有効。

<u>再現手順</u>:

1. に移動 **ストア/設定/B2B 機能/会社を有効にする** および **共有カタログ**.
1. 実行 `bin/magento cron:run`.
1. シンプルな製品を作成し、をクリックします。 **詳細価格**&#x200B;を追加し、 **カタログと階層の価格**&#x200B;を選択して保存します。
1. に移動 **カタログ/共有カタログ/価格と構造を設定**&#x200B;をクリックします。 **設定**&#x200B;を選択し、そのドロップダウンメニューから、すべてのオプションの選択を解除して保存します。
1. 実行 `bin/magento cron:run`.
1. 上記で作成した製品を開き、詳細価格を確認します。

<u>期待される結果</u>:

期待どおりに、パブリック共有カタログからすべての製品を削除した後は、階層価格を製品から削除しないでください。

<u>実際の結果</u>:

階層価格は、公開共有カタログからすべての製品を削除した後に削除されます。


## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
