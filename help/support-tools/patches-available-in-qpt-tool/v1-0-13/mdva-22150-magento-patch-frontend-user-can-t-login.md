---
title: 「MDVA-22150 Adobe Commerce パッチ：フロントエンドユーザーがログインできない」
description: MDVA-22150 パッチは、フロントエンドユーザーがクーポンを使用して購入を中止した後にログインできない問題を解決します。 この問題は、フロントエンドユーザーが購入を完了する前に無効にした製品のクーポンコードを使用した場合に発生します。 その結果、フロントエンドユーザーはログインできなくなり、503 エラーが返されます。 この問題のもう 1 つの影響は、管理者で顧客の買い物かごを管理する機能が機能しなくなることです。
exl-id: 8aabe7b2-4b8a-4339-914e-7131006907b3
feature: Communications
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# MDVA-22150 Adobe Commerce パッチ：フロントエンドユーザーがログインできない

MDVA-22150 パッチは、フロントエンドユーザーがクーポンを使用して購入を中止した後にログインできない問題を解決します。 この問題は、フロントエンドユーザーが購入を完了する前に無効にした製品のクーポンコードを使用した場合に発生します。 その結果、フロントエンドユーザーはログインできなくなり、503 エラーが返されます。 この問題のもう 1 つの影響は、管理者で顧客の買い物かごを管理する機能が機能しなくなることです。

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.13 がインストールされています。 この問題は、Adobe Commerce バージョン 2.3.4 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー上のAdobe Commerce 2.3.2

**Adobe Commerce バージョンとの互換性：** クラウドインフラストラクチャー上のAdobe CommerceとAdobe Commerce 2.3.1 - 2.3.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順：</u>

1. 管理者にログインし、設定可能な製品を作成します。
1. に移動 **買い物かごルール**、およびいくつかの割引を使用してクーポンコードを作成します。
1. フロントエンドに顧客アカウントを作成します。
1. 商品を買い物かごに追加し、チェックアウトプロセスに従って、クーポンを入力します。
1. クーポンを入力した後、注文を送信せずに、注文を中止してログアウトします。
1. 管理者に戻り、設定可能な製品全体を無効にします。

<u>期待される結果：</u>

商品がストアフロントのカートに表示されないか、商品が期待どおりに無効になったことを示す適切なエラーメッセージが表示されます。

<u>実際の結果：</u>

* フロントエンドにログインし直そうとすると、無限ループに陥ります（長い時間が経過すると、最終的に例外が表示されます）。
* 管理者で顧客の買い物かごを管理する機能が動作しなくなります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
