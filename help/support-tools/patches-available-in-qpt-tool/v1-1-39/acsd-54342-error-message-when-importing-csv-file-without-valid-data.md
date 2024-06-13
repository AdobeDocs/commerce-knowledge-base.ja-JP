---
title: 「ACSD-54342：有効なデータのない CSV ファイルを読み込む場合のエラーメッセージ」
description: ACSD-54342 パッチを適用すると、有効なデータのない CSV ファイルを読み込む際に誤ったエラーメッセージが発生するAdobe Commerceの問題を修正できます。
feature: Roles/Permissions
role: Admin, Developer
exl-id: 7f443ad8-c4b7-4294-b38f-9861e221bef2
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# ACSD-54342：有効なデータのない CSV ファイルを読み込む場合のエラーメッセージ

ACSD-54342 パッチでは、有効なデータがない状態で CSV ファイルを読み込むと誤ったエラーメッセージが表示される問題が修正されています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.39 がインストールされています。 パッチ ID は ACSD-54342 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

有効なデータのない CSV ファイルを読み込むと、誤ったエラーメッセージが表示される。

<u>再現手順</u>:

1. 無効なデータのみを含むインポートファイルを作成（例： [!DNL SKUs] 存在しない、顧客アドレスフィールドが無効である、顧客メールアドレスの形式が正しくない）。
1. ファイルを読み込み、を選択して検証エラーをスキップします。

<u>期待される結果</u>:

検証が次の条件で失敗します `There are no valid rows to import` メッセージ。

<u>実際の結果</u>:

検証は成功しますが、読み込みは次のエラーで失敗します `Error in data structure: values are mixed` メッセージ。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
