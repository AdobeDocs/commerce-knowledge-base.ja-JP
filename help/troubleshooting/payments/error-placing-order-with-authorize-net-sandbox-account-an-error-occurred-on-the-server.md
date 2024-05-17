---
title: Authorize.net サンドボックスアカウントへの注文でエラーが発生しました（サーバーでエラーが発生しました）
description: この記事では、Authorize.Net Direct Post を使用して注文する際に表示される「*サーバーでエラーが発生しました*」エラーメッセージの修正について説明します。
exl-id: 764a550a-3373-483c-843d-d8c848dcee35
feature: Compliance, Console, Customer Service, Orders, Payments
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# Authorize.net サンドボックスアカウントへの注文でエラーが発生しました（サーバーでエラーが発生しました）

この記事では、「」の修正について説明します&#x200B;*サーバーでエラーが発生しました*「Authorize.Net Direct Post を使用して注文する際にエラーメッセージが表示される。

>[!WARNING]
>
>**非推奨のお知らせ**
>
>支払いサービスの指示により [PSD2](https://docs.magento.com/user-guide/v2.3/stores/compliance-payment-services-directive.html) そして、多くの API の継続的な進化により、Authorize.Net は将来的に時代遅れになり、セキュリティへの準拠を失うリスクがあります。 このため、現在は非推奨となっており、Adobe Commerce設定で無効にして、対応するに移行することをお勧めします [Commerce Marketplace拡張機能](https://marketplace.magento.com/extensions.html).
>
>**この統合はAdobe Commerce 2.4.0 リリースから削除され、現在のバージョンの 2.3 からは廃止されました。**
>
>非推奨（廃止予定）の支払い統合から安全に移行する方法について詳しくは、 [DevBlog](https://community.magento.com/t5/Magento-DevBlog/Deprecation-of-Magento-core-payment-integrations/ba-p/426445).

## 問題

を使用した注文 [Authorize.Net 直接投稿](https://docs.magento.com/user-guide/v2.3/payment/authorize-net-direct-post.html) サンドボックスアカウントが原因で次のエラーメッセージが表示される：

>>
「サーバーでエラーが発生しました。 もう一度注文してみてください」

## 原因 1: テスト モードが有効になっています

明白ではないようですが、Authorize.net は **テストモード** 設定はに設定する必要があります **不可** サンドボックスアカウントを使用してテストする場合も同様です。

## 解決策 1：テストモードを無効にする

1. に移動 **ストア** > **設定** > **売上** > **支払い方法** > **その他のお支払方法** > **Authorize.net Direct Post**.
1. を設定 **テストモード** 「いいえ」に（チェックを外す） **システム値を使用**&#x200B;を選択し、メニューの「いいえ」を選択します）。
1. クリック **設定を保存**.

![authorize-net_test-mode_setting.png](/help/troubleshooting/miscellaneous/assets/authorize-net_test-mode_setting.png)

## 原因 2：間違った URL

Authorize.net設定には、重要な Authorize.Net リソースの間違った URL アドレスが含まれている可能性があります。

## 解決策 2：正しい URL を指定する

* **ゲートウェイ URL:**   `https://test.authorize.net/gateway/transact.dll`
* **トランザクションの詳細 URL:**   `https://apitest.authorize.net/xml/v1/request.api`
* **API リファレンス：**   `https://developer.authorize.net/api/reference/`

## 何も役に立たなかった場合：デバッグ情報を取得する

Authorize.netでの注文が失敗し、情報が得られない *「異常が発生しました」* エラー、Adobe Commerceを確認してください `debug.log`.

### Transact.dll

この場合、 `debug.log` が空である場合は、 **transact.dll** web ブラウザーのコンソールでの応答：

1. コンソールを開きます。
1. 注文する前に、 **ネットワーク** tab キーを押して選択 **ログを保持**.    ![web-console_network_preserve-log.png](assets/web-console_network_preserve-log.png)
1. 回答のフィルター基準 **transact.dll** エラーの可能性がある応答メッセージを確認します。    ![transact-dll_web-console_response.png](assets/transact-dll_web-console_response.png)
