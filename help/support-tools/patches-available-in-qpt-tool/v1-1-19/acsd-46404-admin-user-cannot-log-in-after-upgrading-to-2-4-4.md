---
title: 「ACSD-46404：管理者ユーザーは、2.4.4 にアップグレードした後にログインできない」
description: ACSD-46404 パッチは、管理者ユーザーが 2.4.4 にアップグレードした後にログインできない問題を解決します。このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.19 がインストールされている場合に利用できます。 パッチ ID は ACSD-46404 です。 この問題はAdobe Commerce 2.4.5 で修正されました。
exl-id: 0aebc879-1128-4be2-a6a8-90d5812c7602
feature: Admin Workspace
role: Admin
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# ACSD-46404：管理者ユーザーは、2.4.4 にアップグレードした後、ログインできない

ACSD-46404 パッチは、管理者ユーザーが 2.4.4 にアップグレードした後にログインできない問題を解決します。このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.19 がインストールされています。 パッチ ID は ACSD-46404 です。 この問題はAdobe Commerce 2.4.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.4-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーは、2.4.4 にアップグレードした後はログインできません。

<u>再現手順</u>:

1. 管理パネルにログインします
1. ストア/に移動します。 **設定** > **設定** > **詳細** > **システム** > **セキュリティ**.
1. 管理者の最大セッションサイズをに設定します **0** 保存します。

<u>期待される結果</u>:

管理者ユーザーは、正常にログインできます。

<u>実際の結果</u>:

管理者ユーザーはログアウトされ、ログインできません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
