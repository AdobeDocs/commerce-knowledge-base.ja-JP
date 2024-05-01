---
title: 「ACSD-54060：制限付き管理者は、別の製品の子である製品を保存できない」
description: ACSD-54060 パッチを適用すると、制限付きの管理者が、別のスコープに割り当てられた別の商品の子である場合に、商品を保存できないAdobe Commerceの問題を修正できます。
feature: Admin Workspace, Roles/Permissions, Products
role: Admin, Developer
exl-id: 28fa3c99-f2b6-4c6d-955a-bd6638a1b077
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# ACSD-54060：制限付き管理者は、別の製品の子である製品を保存できません

ACSD-54060 パッチは、制限された管理者が、別の範囲に割り当てられた別の製品の子である場合に、製品を保存できない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.42 がインストールされています。 パッチ ID は ACSD-54060 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

制限付きの管理者は、製品が、別の範囲に割り当てられた別の製品の子である場合、製品を保存できません。

<u>再現手順</u>:

1. 追加の web サイトを作成します。
1. シンプルな製品を作成して、両方の web サイトに割り当てます。
1. シンプルな製品を唯一のバリエーションとして設定可能な製品を作成し、設定可能な製品をデフォルトの web サイトにのみ割り当てます。
1. 2 つ目の web サイトにのみアクセスできる、制限付きの管理者ユーザーを作成します。
1. 制限付きの管理者ユーザーとしてログインします。
1. 2 つ目の web サイト範囲で、シンプルな製品名を変更してみてください。

<u>期待される結果</u>:

制限付きの管理者は、製品名を変更できます。

<u>実際の結果</u>:

エラーが発生しました： *この項目を表示するには、さらに権限が必要です*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
