---
title: 「MDVA-41061：製品が管理者から保存されると、在庫ステータスが販売可能にリセットされる」
description: MDVA-41061 パッチは、製品が管理者から保存されたときに在庫ステータスが販売可能にリセットされる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-41061。 最新のパッチバージョンは、MDVA-41061-V3 パッチ ID を使用した QPT 1.1.15 で入手できます。 この問題はAdobe Commerce 2.4.4 で修正されていることに注意してください。
exl-id: fd71d3e5-685f-4987-b7e7-bfd86810d865
feature: Admin Workspace, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# MDVA-41061：製品が管理者から保存されると、在庫ステータスが販売可能にリセットされる

MDVA-41061 パッチは、製品が管理者から保存されたときに在庫ステータスが販売可能にリセットされる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.1.5 がインストールされている場合に使用できます。 パッチ ID は MDVA-41061。 最新のパッチバージョンは、MDVA-41061-V3 パッチ ID を使用した QPT 1.1.15 で入手できます。 この問題はAdobe Commerce 2.4.4 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.2-p2、2.4.3 ～ 2.4.3-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫ステータスが、管理者から製品が保存されると販売可能にリセットされる。

<u> 前提条件 </u>:

インベントリモジュールがインストールされます。

<u> 再現手順 </u>:

1. Qty = 1 のシンプル製品を作成します。
1. 手順 1 で作成した製品を使用して注文します。
1. Cron を実行 – キューが実行され `inventory.reservations.updateSalabilityStatus` 製品の在庫ステータスが `cataloginventory_stock_status` テーブルでゼロに変更されていることを確認します。
1. フロントエンドで製品を確認します。 「在庫切れ **とマークする必要があ** ます。
1. 変更せずに製品を管理者に保存します。

<u> 期待される結果 </u>:

* 在庫ステータスは更新しないでください。
* 製品は、フロントエンドで **在庫切れ** になります。

<u> 実際の結果 </u>:

* シンプルな製品は、フロントエンドで **在庫中** とマークされます。
* 買い物かごに追加しようとすると、ユーザーに *リクエストされた数量は使用できません* というメッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
