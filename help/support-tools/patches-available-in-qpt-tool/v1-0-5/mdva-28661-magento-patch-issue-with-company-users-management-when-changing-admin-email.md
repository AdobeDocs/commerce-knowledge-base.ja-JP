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

MDVA-28861 パッチは、管理者の電子メールを変更するときにユーザーにエラーが発生する問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.5 がインストールされている場合に使用できます。 パッチ ID は MDVA-28861。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0 から 2.4.1 （2.3.5-p1 を含む）（B2B 拡張機能を使用）

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

**会社管理者** メールアドレスを変更すると、エラーが返され、**会社ユーザー** リストは表示されません。

<u> 再現手順 </u>:

1. 会社の機能を有効にする（詳しくは、[Commerce管理者での B2B 機能を有効にする：](https://devdocs.magento.com/extensions/b2b/#enable-b2b-features-in-magento-admin) の開発者向けドキュメントを参照し、管理者と 2 人のユーザー（すべてメールアドレスを持つ）から 2 人のユーザーで新しい会社を作成します。
1. **Commerce管理者** / **顧客** / **会社** に移動し、会社アカウントを開きます。
1. **会社管理者** タブを開き、管理者を最初のユーザーに変更します。これには、**会社管理者** のメールを最初のユーザーのメールに変更することも含まれます。
1. Adobe Commerce フロントエンドに移動し、最初のユーザーとしてログインします。
1. **会社ユーザー** セクションに移動します。

<u> 期待される結果 </u>:

**会社ユーザー** リストが期待どおりに表示されます。

<u> 実際の結果 </u>:

**会社ユーザー** リストは表示されず、次のようなエラーが表示されます。

```bash
No such entity with id = 2
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。

B2B 会社の機能について詳しくは、開発者向けドキュメントで次の記事を参照してください。

* [B2B デベロッパーガイド ](https://devdocs.magento.com/guides/v2.4/b2b/bk-b2b.html)
* [ 会社の役割の管理 ](https://devdocs.magento.com/guides/v2.4/b2b/roles.html)
* [Adobe Commerce Enterprise B2B Extension 設定パスのリファレンス ](https://devdocs.magento.com/guides/v2.4/config-guide/prod/config-reference-b2b.html)
