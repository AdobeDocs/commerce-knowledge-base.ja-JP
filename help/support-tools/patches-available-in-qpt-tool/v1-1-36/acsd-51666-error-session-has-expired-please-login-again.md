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

# ACSD-51666: エラー *セッションの有効期限が切れています。もう一度ログインしてください。ログイン後の*

ACSD-51666 パッチにより、*セッションの有効期限が切れました。もう一度ログインしてください。ログインを試みた後に* が発生します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.36 がインストールされている場合に使用できます。 パッチ ID は ACSD-51666 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「セッションの有効期限が切れました。もう一度ログインしてください *」というエラーが表示される。別のデバイスでパスワードをリセットした後に、あるデバイスから新しいパスワードでログインしようとすると、* が発生します。 カスタムモジュールによって追加されたページに追加の Ajax リクエストがある場合にのみ発生します。

<u> 再現手順 </u>:

1. ストアフロントの各ページに Ajax リクエストを追加するカスタムモジュールをインストールします。
1. 新しいアカウントを作成します。
1. ログアウトして、ログインページに戻ります。
1. *パスワードを忘れた場合* リンクを別のブラウザーで開き、*パスワードをリセット* メールを送信します。
1. 最初のブラウザーでパスワードリセットメールを開き、新しいパスワードを設定します。
1. 2 つ目のブラウザーでログインしてみてください。

<u> 期待される結果 </u>:

最初の試行で正常にログインできます。

<u> 実際の結果 </u>:

* *セッションの有効期限が切れています。もう一度ログインしてください。* エラー。
* ログインせず、ホームページにリダイレクトされる。
* 2 回目のログインは成功しました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
