---
title: 「MDVA-33976 パッチ：オプションの削除後にバンドルが在庫切れになる」
description: MDVA-33976 パッチは、バンドル製品のオプションのいずれかが管理者で削除された後、その製品が在庫切れと表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） 1.0.15] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp）がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 2e2bc05b-ad31-4e87-b33e-3526f6a42478
feature: Orders
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# MDVA-33976 パッチ：オプションを削除した後、バンドルが在庫切れになる

MDVA-33976 パッチは、バンドル製品のオプションのいずれかが管理者で削除された後、その製品が在庫切れと表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） 1.0.15](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.3 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce on-premises 2.3.0-2.3.6-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. Commerce Admin でバンドル製品を開きます。
1. バンドル製品オプションの 1 つを削除します。
1. 変更を保存します。
1. ストアフロントで商品を開きます。

<u> 期待される結果 </u>:

バンドル製品の在庫ステータスは、子製品の在庫ステータスに従って更新されます。

<u> 実際の結果 </u>:

子製品のステータスに関係なく、バンドル製品は「在庫切れ」と表示されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
