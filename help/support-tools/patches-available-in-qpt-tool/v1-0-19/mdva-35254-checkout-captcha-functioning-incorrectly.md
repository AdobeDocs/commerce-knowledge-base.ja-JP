---
title: 「MDVA-35254:CAPTCHA が正しく機能していないチェックアウト」
description: MDVA-35254 パッチは、サードパーティの支払いのチェックアウトが失敗した後、CAPTCHA フィールドが表示されない問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-35254。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: 226c672b-3740-4a87-9ea1-66892acb9fe2
feature: Checkout, Orders
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# MDVA-35254:CAPTCHA が正しく機能していないチェックアウト

MDVA-35254 パッチは、サードパーティの支払いのチェックアウトが失敗した後、CAPTCHA フィールドが表示されない問題を修正しました。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.19 がインストールされています。 パッチ ID は MDVA-35254。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.1～2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

CAPTCHA の設定：

1. サードパーティの支払いプロバイダーをインストールして設定します（例：Braintree）。
1. に移動 **ストア/設定/カスタマー/カスタマー設定/CAPTCHA/Forms**.
1. を選択 **チェックアウト/注文**.
1. 保持： **ログインに失敗した回数** デフォルトとして（デフォルト = *3*）に設定します。
1. 顧客としてログインします。
1. 商品を買い物かごに追加します。
1. チェックアウトの支払いセクションに移動します。
1. を選択 **クレジットカード** 支払方法（例：Braintree）。
1. 3 回失敗した支払いを試みます。

<u>期待される結果</u>:

CAPTCHA フィールドは、失敗した試行回数に達すると表示されます。

<u>実際の結果</u>:

CAPTCHA フィールドは表示されず、次のエラーメッセージのみが表示されます。 *CAPTCHA コードを指定して、もう一度試してください。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
