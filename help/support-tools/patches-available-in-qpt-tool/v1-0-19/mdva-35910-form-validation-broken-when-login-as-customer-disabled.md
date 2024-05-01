---
title: 「MDVA-35910:「顧客としてログイン」が無効な場合にフォームの検証が壊れる」
description: MDVA-35910 パッチでは、「**顧客としてログイン**」拡張機能が無効な場合に顧客アカウントを作成フォームの検証が機能しない問題が解決されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-35910。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: fa63d725-33f0-4422-bcd5-d62dfee01b65
feature: Cache
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# MDVA-35910:[ 顧客としてログイン ] が無効な場合にフォームの検証が壊れる

MDVA-35910 パッチは、次の場合に顧客アカウント作成フォームの検証が機能しない問題を解決します。 **顧客としてログイン** 拡張機能が無効になっています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.19 がインストールされています。 パッチ ID は MDVA-35910。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.1～2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. に移動します。 **ストア/設定/顧客**. 無効 **顧客としてログイン** admin.
1. 次の下 **顧客としてログイン**、設定 **拡張機能を有効にする** = *不可*.
1. 設定を保存し、キャッシュをフラッシュします。
1. ストアフロントに戻り、をクリックします **登録** （顧客アカウントを作成します）。
1. アカウントフォームに入力し、以下の検証が行われたかどうかを確認します **メールを確認** 動作しているかどうか。

<u>期待される結果</u>:

顧客アカウントの作成プロセスはエラーなしで完了します。

<u>実際の結果</u>:

顧客アカウントの作成プロセスが完了せず、代わりに Javascript コンソールエラーが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
