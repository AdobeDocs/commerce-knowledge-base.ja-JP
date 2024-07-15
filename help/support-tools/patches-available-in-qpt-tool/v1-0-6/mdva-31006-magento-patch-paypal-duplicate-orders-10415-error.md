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

MDVA-31006 パッチは、PayPal Express のチェックアウト支払いを使用すると、10415 エラーで重複した注文が作成される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.6 がインストールされている場合に使用できます。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.4.0

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーはAdobe Commerce注文成功ページに送信されないので、空白ページが更新され、2 回目の注文が行われて、重複した注文が発生します。

<u> 前提条件 </u>:

* Adobe Commerceがインストールされました。
* PayPal Express のチェックアウト支払いが設定されます。
* Commerce管理者にログインします。 **Stores**/**Configuration**/**Sales**/**Payment Methods**/**Paypal Express Checkout**/**Configure**/**Advanced Settings**/**Skip Order Review Step**/*No* に移動します。

<u> 再現手順 </u>:

1. ユーザーとしてログインします。
1. 項目を選択し、「**買い物かごに追加**」をクリックします。
1. 買い物かごをクリックし、**チェックアウトに進む** をクリックします。
1. PayPal Express ウィンドウに進み、支払いを行います。
1. Adobe Commerceの注文のレビューページにリダイレクトされます。
1. **Place Order** ボタンを押します。
1. サーバーインフラストラクチャの問題によるシステムエラーをエミュレートします。 空白のページが表示されます。
1. ページを更新します。

<u> 期待される結果 </u>:

* お客様は注文の確認ページにリダイレクトされ、「*支払い処理が正常に完了しました。 ご注文されたかどうかご確認ください。*」
* `/var/log/payment.log` にある payment.log にはエラー 10415 がありますが、1 つの注文のみが作成されました。

<u> 実際の結果 </u>:

* お客様がAdobe Commerce注文成功ページに送信されないので、空白ページが更新され、2 回目の注文が行われて、重複した 2 つの注文が作成されます。
* `/var/log/payment.log` にある payment.log には、エラー 10415 があります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
