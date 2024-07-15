---
title: 「MDVA-43824：注文のキャンセルアクションが失敗し、「項目がキャンセルされていません」というエラーが表示される」
description: 「MDVA-43824 パッチは、注文のキャンセル操作が次のエラーで失敗した問題を解決します：*アイテムをキャンセルしていません*。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.13 がインストールされている場合に利用できます。 パッチ ID は MDVA-43824。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。'
exl-id: e4d839d6-84ed-4157-80a1-fd482fef897c
feature: Orders
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# MDVA-43824：注文のキャンセル操作が失敗し、「アイテムがキャンセルされていません」というエラーが表示される

MDVA-43824 パッチは、注文キャンセル アクションが次のエラーで失敗した問題を解決します。*アイテムをキャンセルしていません*。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.13 がインストールされている場合に使用できます。 パッチ ID は MDVA-43824。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.6 ～ 2.3.7-p3、2.4.1 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ログインしている顧客が行った注文をキャンセルすることはできません。 注文のキャンセル操作が次のエラーで失敗しました：

```
Zend_Db_Statement_Exception: SQLSTATE[23000]: Integrity constraint violation: 1452 Cannot add or update a child row: a foreign key constraint fails (`mer33515_ee24developpbdevelop`.`salesrule_customer`, CONSTRAINT `SALESRULE_CUSTOMER_RULE_ID_SEQUENCE_SALESRULE_SEQUENCE_VALUE` FOREIGN KEY (`rule_id`) REFERENCES `sequence_salesrule` (`sequen), query was: INSERT INTO `salesrule_customer` () VALUES (){code}
```

<u> 再現手順 </u>:

1. 販売ルールを作成します（クーポンタイプは「特定クーポン」または「クーポンなし」です）。
1. ストアフロントに移動して、顧客としてログインし、商品を買い物かごに追加します。
1. 買い物かごに移動し、買い物かご価格ルールに「特定のクーポン」というクーポンがある場合は、買い物かご価格ルールを適用します。 買い物かごの価格ルールが正常に適用されます。
1. チェックアウトに移動し、任意の支払い方法で注文します。
1. Commerce管理者/**営業**/**注文** に移動します。
1. 手順 4 で発注した品目を開きます。
1. 「**キャンセル**」ボタンをクリックします。

<u> 期待される結果 </u>:

注文はエラーなしで正常にキャンセルされました。

<u> 実際の結果 </u>:

注文のキャンセル操作が次のエラーで失敗しました：*品目はキャンセルされていません。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
