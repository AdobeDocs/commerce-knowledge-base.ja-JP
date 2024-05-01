---
title: 「ACSD-54026:updateCompanyRole GraphQL リクエストに対して誤ったエラーメッセージ」
description: ACSD-54026 パッチを適用して、許可されていないユーザーに対する updateCompanyRole GraphQL リクエストに間違ったエラーメッセージが表示されるAdobe Commerceの問題を修正してください。
feature: Roles/Permissions
role: Admin, Developer
exl-id: c18a8815-975a-499d-a372-8635d89aa673
source-git-commit: dccb8dde1666fa0c72c7c94cd94c82daddaadc54
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# ACSD-54026：のエラーメッセージが正しくありません `updateCompanyRole` GraphQL リクエスト

ACSD-54026 パッチは、に対する誤ったエラーメッセージがある問題を修正します。 `updateCompanyRole` 許可されていないユーザーに対するGraphQL リクエスト。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.39 がインストールされています。 パッチ ID は ACSD-54026 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

に対する誤ったエラーメッセージの取得 `updateCompanyRole` 許可されていないユーザーに対するGraphQL リクエスト。

<u>再現手順</u>:

1. 設定で B2B 会社を有効にします。
1. 会社を作成します。
1. 送信 `updateCompanyRole` ベアラートークンを渡さずに、または無効なベアラートークンを指定して、GraphQL リクエストを実行します。
1. GraphQL応答でエラーメッセージを確認します。

<u>期待される結果</u>:

次のエラーメッセージが表示されます。 *現在の顧客は承認されていません。*

<u>実際の結果</u>:

次のエラーメッセージが表示されます。 *顧客は会社のユーザーではありません。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
