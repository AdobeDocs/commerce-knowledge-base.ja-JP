---
title: 「MDVA-40311：カスタム管理パスが設定されている場合、管理者にログインした後に「セキュリティまたはフォームキーが無効です」エラーが発生する」
description: 「MDVA-40311 パッチは、管理者ユーザーが「無効なセキュリティまたはフォームキー」というエラーメッセージを取得する問題を修正します。 カスタム管理パスが設定され、秘密鍵が有効な場合は、管理者にログインした後、ページ*を更新してください。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.7 がインストールされている場合に利用できます。 パッチ ID は MDVA-40311。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。'
exl-id: d4562f09-0aed-438e-8c2e-90557aa2f146
feature: Admin Workspace, Compliance, Security
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# MDVA-40311：カスタム管理パスが設定されている場合、管理者にログインした後に「セキュリティまたはフォームキーが無効です」エラーが発生する

MDVA-40311 パッチは、管理者ユーザが次のエラーメッセージを取得する問題を修正します。 *セキュリティまたはフォーム キーが無効です。 ページを更新してください*&#x200B;に移動します。管理者にログインした後、カスタム管理パスが設定され、秘密鍵が有効になっている場合に限ります。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.7 がインストールされています。 パッチ ID は MDVA-40311。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーに次のエラーメッセージが表示される： *セキュリティまたはフォーム キーが無効です。 ページを更新してください*&#x200B;に移動します。管理者にログインした後、カスタム管理パスが設定され、秘密鍵が有効になっている場合に限ります。

<u>再現手順</u>:

* 有効なユーザー名とパスワードを使用して、管理者ユーザーとしてログインします。

<u>期待される結果</u>:

ユーザーはエラーメッセージなしでログインできる。

<u>実際の結果</u>:

*セキュリティまたはフォーム キーが無効です。 ページを更新してください* エラーメッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
