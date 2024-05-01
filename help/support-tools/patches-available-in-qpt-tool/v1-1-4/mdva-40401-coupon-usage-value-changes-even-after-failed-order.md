---
title: 「MDVA-40401：注文に失敗すると、クーポンの使用価値が変更される」
description: MDVA-40401 パッチは、注文に失敗した後もクーポンの使用値が変更される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.4 がインストールされている場合に利用できます。 パッチ ID は MDVA-40401。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: c497ee84-9c20-4c75-ad3a-3b71f699acbf
feature: Orders
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# MDVA-40401：注文に失敗すると、クーポンの使用価値が変更される

MDVA-40401 パッチは、注文に失敗した後もクーポンの使用値が変更される問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.1.4 がインストールされています。 パッチ ID は MDVA-40401。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.6 ～ 2.3.7-p2、2.4.1 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーは、失敗した順序でクーポンを使用すると、クーポンを再適用できません。

<u>再現手順</u>:

1. 自動生成されたクーポンを含む買い物かごルールを作成します。
1. 商品を買い物かごに追加し、クーポンを適用します。
1. に移動 **チェックアウト**.
1. 注文する前に、追加した製品を「在庫切れ」にします。
1. 以下を取得する必要があります。 *在庫切れ* エラー。
1. cron を実行します。
1. 買い物かごに移動し、その製品を削除します。
1. 別の製品を追加してクーポンを適用します。

<u>期待される結果</u>:

以前の注文が行われなかったので、クーポンコードは正常に適用されます。

<u>実際の結果</u>:

A が表示されます *クーポンコードが無効です* エラー。

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
