---
title: 「MDVA-29954：間違ったアドレスが新しい会社ユーザー登録メールを送信しました」
description: MDVA-29954 パッチを使用すると、「新しい会社の登録リクエスト」と「会社へのリンクが完了しました」というメールが、誤ったメールアドレスから送信される問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.8 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 9b3d1b93-3fe6-40a0-a68a-3e3d789c6d66
feature: B2B, Communications, Companies
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# MDVA-29954：間違ったアドレスが新しい会社ユーザー登録メールを送信しました

MDVA-29954 パッチを使用すると、「新しい会社の登録リクエスト」と「会社へのリンクが完了しました」というメールが、誤ったメールアドレスから送信される問題を解決できます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.8 がインストールされています。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.5-p2、2.4.0、2.4.1。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>前提条件</u>:

B2B と共にAdobe Commerceをインストール **B2B の機能** および **会社** 有効。

<u>再現手順</u>:

1. 「」をクリック **アカウントを作成** ストアフロントのドロップダウンで、 **新しい会社アカウントを作成**.
1. 必須フィールドに入力し、アカウントを登録します。
1. を有効にする **会社** バックエンドから（**顧客** > **会社**）に設定します。
1. 登録に使用したメールアドレスを確認します。
1. を **会社の管理者パスワード** メールで送信された手順に従います。
1. でフロントエンドにログインします。 **会社の管理者パスワード**.
1. 新しいを作成 **会社ユーザー** 。対象： **マイアカウント** > **会社のユーザー** > **新規ユーザーの追加**.
1. に移動 **ストア** > **設定** > **一般ストアのメールアドレス** > **一般連絡先**、およびチェック **送信者のメール**.
1. の登録に使用したメールに移動します **新規ユーザー** 手順 7 の場合。

<u>期待される結果</u>:

「あなたは会社にリンクされています」というメールが、と同じ値のメールアドレスから送信されます **送信者のメール** 手順 8 の場合。

<u>実際の結果</u>:

「あなたは会社にリンクされています」というメールが **会社管理者** 電子メール。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
