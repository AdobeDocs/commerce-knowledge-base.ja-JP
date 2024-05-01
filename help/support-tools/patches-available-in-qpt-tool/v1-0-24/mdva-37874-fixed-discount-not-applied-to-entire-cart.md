---
title: 「MDVA-37874：買い物かご全体に固定割引が適用されない」
description: MDVA-37874 パッチは、複数のオプションを含むバンドル製品にカート全体の**固定割引額**が誤って適用された場合の問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.24 がインストールされている場合に利用できます。 パッチ ID は MDVA-37874。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。
exl-id: a1c414f0-b654-4b18-b502-47351513ddfa
feature: Orders, Personalization, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# MDVA-37874：買い物かご全体に適用されない固定割引

MDVA-37874 パッチにより、 **固定割引金額** 買い物かご全体について、複数のオプションを含むバンドル製品に誤って適用されます。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.24 がインストールされています。 パッチ ID は MDVA-37874。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

* このパッチは、クラウドインフラストラクチャ 2.4.2 上のAdobe Commerce用に設計されました
* また、このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.6-2.3.7 と 2.4.1-2.4.2-p1 とも互換性があります

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題


<u>再現手順</u>:

1. で買い物かごルールを作成します **固定割引金額** 買い物かご全体に対して。
1. バンドル製品を買い物かごに追加します（バンドル製品には、選択した複数のオプションが含まれている必要があります）。
1. 買い物かごページに移動し、割引を確認します。


<u>期待される結果</u>:

固定割引額は、期待どおりに買い物かご全体に適用されます。

<u>実際の結果</u>:

固定割引額は、買い物かごの一部にのみ適用されます。


## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
