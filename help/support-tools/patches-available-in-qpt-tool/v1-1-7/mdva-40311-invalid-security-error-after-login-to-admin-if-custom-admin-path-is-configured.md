---
title: 「MDVA-40311：カスタム管理パスが設定されている場合、管理者にログインした後に「セキュリティまたはフォームキーが無効です」エラーが発生する」
description: 「MDVA-40311 パッチは、管理者ユーザーが「無効なセキュリティまたはフォームキー」というエラーメッセージを取得する問題を修正します。 カスタム管理パスが設定され、秘密鍵が有効な場合は、管理者にログインした後、ページ*を更新してください。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.7 がインストールされている場合に利用できます。 パッチ ID は MDVA-40311。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。'
exl-id: d4562f09-0aed-438e-8c2e-90557aa2f146
feature: Admin Workspace, Compliance, Security
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# MDVA-40311：カスタム管理パスが設定されている場合、管理者にログインした後に「セキュリティまたはフォームキーが無効です」エラーが発生する

MDVA-40311 パッチは、管理者ユーザーが *無効なセキュリティまたはフォームキーというエラーメッセージを取得する問題を修正します。 カスタム管理パスが設定され* 秘密鍵が有効な場合は、管理者にログインした後、ページを更新してください。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.7 がインストールされている場合に使用できます。 パッチ ID は MDVA-40311。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーに「*セキュリティまたはフォームキーが無効です。 カスタム管理パスが設定され* 秘密鍵が有効な場合は、管理者にログインした後、ページを更新してください。

<u> 再現手順 </u>:

* 有効なユーザー名とパスワードを使用して、管理者ユーザーとしてログインします。

<u> 期待される結果 </u>:

ユーザーはエラーメッセージなしでログインできる。

<u> 実際の結果 </u>:

*セキュリティまたはフォームキーが無効です。 ページを更新してください。エラーメッセージ* 表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
