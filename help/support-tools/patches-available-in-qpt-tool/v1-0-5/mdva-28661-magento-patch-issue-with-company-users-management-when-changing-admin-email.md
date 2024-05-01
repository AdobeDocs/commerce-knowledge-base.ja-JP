---
title: 「MDVA-28661：管理者メールを変更する際の会社ユーザー管理の問題」
description: MDVA-28861 パッチは、管理者の電子メールを変更するときにユーザーにエラーが発生する問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-28861。
exl-id: 2d6691e5-baaf-4cef-ae7e-2b6ccc7f2cd3
feature: Admin Workspace, Communications, Companies
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# MDVA-28661：管理者の電子メールを変更する際の会社ユーザー管理の問題

MDVA-28861 パッチは、管理者の電子メールを変更するときにユーザーにエラーが発生する問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.5 がインストールされています。 パッチ ID は MDVA-28861。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0 から 2.4.1 （2.3.5-p1 を含む）（B2B 拡張機能を使用）

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

変更後： **会社管理者** メールアドレスにエラーが返され、 **会社のユーザー** リストが表示されない。

<u>再現手順</u>:

1. 会社機能を有効にする（詳しくは、こちらを参照） [B2B のインストール：Commerce Admin での B2B 機能の有効化](https://devdocs.magento.com/extensions/b2b/#enable-b2b-features-in-magento-admin) アドビの開発者ドキュメントでは、2 人のユーザー（管理者と 2 人のユーザー）で新しい会社を作成し、全員がメールアドレスを持っています。
1. に移動します **Commerce管理者** > **顧客** > **会社** そして会社アカウントを開きます。
1. 開く **会社管理者** 最初のユーザーに tab キーを押して「admin」を変更します。これには、次の変更が含まれます **会社管理者** 最初のユーザーのメールに送信します。
1. Adobe Commerce フロントエンドに移動し、最初のユーザーとしてログインします。
1. に移動します **会社のユーザー** セクション。

<u>期待される結果</u>:

この **会社のユーザー** リストは、期待どおりに表示されます。

<u>実際の結果</u>:

この **会社のユーザー** リストが表示されず、次のようなエラーが表示されます。

```bash
No such entity with id = 2
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。

B2B 会社の機能について詳しくは、開発者向けドキュメントで次の記事を参照してください。

* [B2B デベロッパーガイド](https://devdocs.magento.com/guides/v2.4/b2b/bk-b2b.html)
* [会社の役割の管理](https://devdocs.magento.com/guides/v2.4/b2b/roles.html)
* [Adobe Commerce Enterprise B2B Extension 設定パスのリファレンス](https://devdocs.magento.com/guides/v2.4/config-guide/prod/config-reference-b2b.html)
