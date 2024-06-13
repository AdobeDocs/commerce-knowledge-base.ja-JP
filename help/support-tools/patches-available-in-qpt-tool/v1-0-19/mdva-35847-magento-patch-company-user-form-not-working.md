---
title: 「MDVA-35847：会社ユーザーフォームが機能しない」
description: MDVA-35847 パッチは、会社ユーザーフォームが機能せず、フロントエンドで 500 エラーを返す問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-35847。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: 1a3f4a61-0c21-460a-ae48-e792d03ed805
feature: B2B, Companies
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# MDVA-35847：会社ユーザーフォームが機能しない

MDVA-35847 パッチは、会社ユーザーフォームが機能せず、フロントエンドで 500 エラーを返す問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.19 がインストールされています。 パッチ ID は MDVA-35847。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.1～2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>前提条件</u>:

Adobe Commerce B2B がインストールされています。

<u>再現手順</u>:

1. に移動 **ストア** > **属性** > **顧客**&#x200B;を選択し、新しいカスタム顧客属性を作成します。

   * 入力タイプ = *日付*
   * ストアフロントに表示= *はい*
   * 並べ替え順= *0*
   * で使用するForms = *すべてのフォーム*

1. 新しい会社を作成します。
1. フロントエンドで会社管理者としてログインします。
1. 会社ユーザーのセクションに移動します。

<u>期待される結果</u>:

会社ユーザーフォームが通常どおり読み込まれます。

<u>実際の結果</u>:

会社ユーザーフォームが読み込まれず、500 エラーが返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
