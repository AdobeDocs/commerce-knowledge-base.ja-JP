---
title: 「ACSD-54472：拒否された会社の顧客は、引き続き認証できます」
description: ACSD-54472 パッチを適用すると、拒否された会社の顧客は引き続き認証でき、ブロックおよび拒否された会社の顧客は引き続き注文できるAdobe Commerceの問題を修正できます。
feature: B2B
role: Admin, Developer
exl-id: 76fc4553-02b1-4563-91a9-0cda99fa4c7d
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# ACSD-54472：拒否された会社の顧客は、引き続き認証できます

ACSD-54472 パッチは、拒否された会社の顧客が引き続き認証でき、ブロックされて拒否された会社の顧客が引き続き注文できる問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされています。 パッチ ID は ACSD-54472 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

拒否された会社の顧客は引き続き認証でき、ブロックされて拒否された会社の顧客は引き続き注文できます。

<u>再現手順</u>:

1. 会社を作成します。
1. 次を経由して商品を買い物かごに追加 [!DNL GraphQL].
1. 会社ステータスの変更 *ブロック*.
1. を送信 [!DNL GraphQL] 注文を行い、譲渡可能な見積もりを作成するリクエスト。
1. 会社ステータスの変更 *却下*.
1. を送信 [!DNL GraphQL] 会社のユーザー認証トークンを取得するリクエスト。
1. 顧客ステータスを次のように設定： *Inactive*.
1. を送信 [!DNL GraphQL] 会社のユーザー認証トークンを取得するリクエスト。

<u>期待される結果</u>:

* のユーザーが注文および交渉可能な見積もりを行っていない *ブロック* 会社
* のユーザーについて、認証トークンが取得されていません *却下* 会社
* に対する認証トークンが取得されていません *Inactive* 顧客。

<u>実際の結果</u>:

* 注文および交渉可能な見積もりは、 *ブロック* 会社
* のユーザー用に認証トークンが取得されます *却下* 会社
* の認証トークンが取得されました *Inactive* 顧客。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
