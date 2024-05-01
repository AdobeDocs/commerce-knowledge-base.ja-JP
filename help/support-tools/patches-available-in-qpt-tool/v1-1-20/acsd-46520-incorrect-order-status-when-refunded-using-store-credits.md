---
title: 「ACSD-46520：ストアクレジットを使用して払い戻した場合の注文ステータスが正しくない」
description: この記事では、ストアクレジットを使用して返金すると、ユーザーに誤った注文ステータスが表示される問題の解決策を説明します。
exl-id: 8464df22-0223-4ded-a15f-ce06eacdf77c
feature: Orders, Returns
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# ACSD-46520：ストアクレジットを使用して払い戻した際の注文ステータスが正しくない

ACSD-46520 パッチは、ストアクレジットを使用して払い戻した際に、ユーザーが誤った注文ステータスを取得する問題を解決します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.20 がインストールされています。 パッチ ID は ACSD-46520 です。 この問題はAdobe Commerce 2.4.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 および 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアクレジットを使用して返金すると、ユーザーに誤った注文ステータスが表示される。

<u>再現手順</u>:

1. ストアフロントで顧客アカウントを作成し、ログインします。
1. 管理者から顧客にストアクレジットを割り当てます。 ストアクレジットは注文全体に適用されます。
1. 店舗クレジットを使用して注文します。
1. 注文を請求します。
1. 注文の全額を返金するクレジットメモを作成します。
「」を選択します **[!UICONTROL Refund to store credit]** チェックボックス。
1. 注文ステータスを確認します。

<u>期待される結果</u>:

注文のステータスは *クローズ*.

<u>実際の結果</u>:

注文のステータスは *完了*。これは正しいステータスではありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe Commerceまたは [!DNL Magento Open Source] オンプレミス： [品質向上パッチ 「ツール」 > 「使用方法」](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) 『品質向上パッチツール』マニュアルの「」を参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/check-patch-for-magento-issue-with-magento-quality-patches.html) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) 『品質向上パッチツール』マニュアルの「」を参照してください。
