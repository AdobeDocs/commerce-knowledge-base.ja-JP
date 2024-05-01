---
title: 'MDVA-31006: Paypal 重複注文 10415 エラー'
description: MDVA-31006 パッチは、PayPal Express のチェックアウト支払いを使用すると、10415 エラーで重複した注文が作成される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.6 がインストールされている場合に利用できます。 この問題は、Adobe Commerce 2.4.2 で修正されました。
exl-id: ff471fd3-f580-4149-83bc-67f6fce8e28d
feature: Orders, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# MDVA-31006: Paypal Duplicate Orders 10415 エラー

MDVA-31006 パッチは、PayPal Express のチェックアウト支払いを使用すると、10415 エラーで重複した注文が作成される問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.6 がインストールされています。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.4.0

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーはAdobe Commerce注文成功ページに送信されないので、空白ページが更新され、2 回目の注文が行われて、重複した注文が発生します。

<u>前提条件</u>:

* Adobe Commerceがインストールされました。
* PayPal Express のチェックアウト支払いが設定されます。
* Commerce管理者にログインします。 に移動 **ストア** > **設定** > **売上** > **支払い方法** > を選択 **Paypal Express チェックアウト** > **設定** > **詳細設定** > **注文レビューステップをスキップ** > *不可*.

<u>再現手順</u>:

1. ユーザーとしてログインします。
1. 項目を選択し、 **カートに追加**.
1. 買い物かごをクリックし、 **チェックアウトに進む**.
1. PayPal Express ウィンドウに進み、支払いを行います。
1. Adobe Commerceの注文のレビューページにリダイレクトされます。
1. を押します。 **注文する** ボタン。
1. サーバーインフラストラクチャの問題によるシステムエラーをエミュレートします。 空白のページが表示されます。
1. ページを更新します。

<u>期待される結果</u>:

* お客様は注文の確認ページにリダイレクトされ、「*正常な支払いトランザクションが既に完了しています。 ご注文されたかどうかをご確認ください。*“
* 次の場所にある payment.log 内 `/var/log/payment.log`、エラー 10415 が発生しましたが、作成された注文は 1 つだけです。

<u>実際の結果</u>:

* お客様がAdobe Commerce注文成功ページに送信されないので、空白ページが更新され、2 回目の注文が行われて、重複した 2 つの注文が作成されます。
* 次の場所にある payment.log 内 `/var/log/payment.log`、エラー 10415 が発生しました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
