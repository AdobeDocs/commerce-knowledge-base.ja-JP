---
title: 「MDVA-41061：製品が管理者から保存されると、在庫ステータスが販売可能にリセットされる」
description: MDVA-41061 パッチは、製品が管理者から保存されたときに在庫ステータスが販売可能にリセットされる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-41061。 最新のパッチバージョンは、MDVA-41061-V3 パッチ ID を使用した QPT 1.1.15 で入手できます。 この問題はAdobe Commerce 2.4.4 で修正されていることに注意してください。
exl-id: fd71d3e5-685f-4987-b7e7-bfd86810d865
feature: Admin Workspace, Orders, Products
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# MDVA-41061：製品が管理者から保存されると、在庫ステータスが販売可能にリセットされる

MDVA-41061 パッチは、製品が管理者から保存されたときに在庫ステータスが販売可能にリセットされる問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.1.5 がインストールされています。 パッチ ID は MDVA-41061。 最新のパッチバージョンは、MDVA-41061-V3 パッチ ID を使用した QPT 1.1.15 で入手できます。 この問題はAdobe Commerce 2.4.4 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.2-p2、2.4.3 ～ 2.4.3-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫ステータスが、管理者から製品が保存されると販売可能にリセットされる。

<u>前提条件</u>:

インベントリモジュールがインストールされます。

<u>再現手順</u>:

1. Qty = 1 のシンプル製品を作成します。
1. 手順 1 で作成した製品を使用して注文します。
1. Cron を実行 – 確認する `inventory.reservations.updateSalabilityStatus` でキューが実行され、製品在庫ステータスがゼロに変更されました `cataloginventory_stock_status` テーブル。
1. フロントエンドで製品を確認します。 としてマークする必要があります。 **在庫切れ**.
1. 変更せずに製品を管理者に保存します。

<u>期待される結果</u>:

* 在庫ステータスは更新しないでください。
* 製品は、 **在庫切れ** フロントエンドで。

<u>実際の結果</u>:

* 単純な製品は次のマークが付いています： **在庫あり** フロントエンドで。
* Users get *リクエストされた数量は使用できません* をカートに追加しようとするとメッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
