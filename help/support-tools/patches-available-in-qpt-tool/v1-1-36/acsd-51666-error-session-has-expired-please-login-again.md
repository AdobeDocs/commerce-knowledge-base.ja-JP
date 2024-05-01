---
title: '「ACSD-51666: エラー「セッションの有効期限が切れています。もう一度ログインしてください。」 ログイン後'''
description: ACSD-51666 パッチを適用して、「セッションの有効期限が切れました。もう一度ログインしてください。」というエラーが表示されるAdobe Commerceの問題を修正してください。*はログインを試みた後に発生します。
feature: Customers
role: Admin, Developer
exl-id: c3913f1c-f401-440b-b6b3-10702f13fff5
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# ACSD-51666: エラー *セッションの有効期限が切れています。もう一度ログインしてください。* ログイン後

ACSD-51666 パッチは、エラーが発生する問題を修正します *セッションの有効期限が切れています。もう一度ログインしてください。* ログインを試みた後に発生します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.36 がインストールされています。 パッチ ID は ACSD-51666 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

次のエラーが発生します *セッションの有効期限が切れています。もう一度ログインしてください。* 別のデバイスでパスワードをリセットした後、あるデバイスから新しいパスワードでログインしようとした場合。 カスタムモジュールによって追加されたページに追加の Ajax リクエストがある場合にのみ発生します。

<u>再現手順</u>:

1. ストアフロントの各ページに Ajax リクエストを追加するカスタムモジュールをインストールします。
1. 新しいアカウントを作成します。
1. ログアウトして、ログインページに戻ります。
1. を開きます *Forgot Password* 別のブラウザーでリンクし、 *パスワードをリセット* 電子メール。
1. 最初のブラウザーでパスワードリセットメールを開き、新しいパスワードを設定します。
1. 2 つ目のブラウザーでログインしてみてください。

<u>期待される結果</u>:

最初の試行で正常にログインできます。

<u>実際の結果</u>:

* 「」が表示されます。 *セッションの有効期限が切れています。もう一度ログインしてください。* エラー。
* ログインせず、ホームページにリダイレクトされる。
* 2 回目のログインは成功しました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
