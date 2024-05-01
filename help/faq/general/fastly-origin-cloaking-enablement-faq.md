---
title: “[!DNL Fastly] オリジンクローキングの有効化に関する FAQ
description: この FAQ では、に関するよくある質問について説明しています。 [!DNL Fastly] Adobe Commerceでのオリジンクロークの有効化（2021 年時点で完全に実装されています）。
exl-id: d608abe7-7d64-44ce-bea1-34b201c29113
source-git-commit: 348a1f6e455aff9ad7c562ea20c95f27c9ee0b86
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# [!DNL Fastly] オリジンクローキングの有効化に関するよくある質問

この FAQ では、に関するよくある質問について説明しています。 [!DNL Fastly] Adobe Commerceでのオリジンクロークの有効化（2021 年時点で完全に実装されています）。

## について [!DNL Fastly] オリジン・クローク？

オリジンクロークは、クラウドインフラストラクチャ上のAdobe Commerceで任意のをブロックできるセキュリティ機能です [!DNL non-Fastly] トラフィック（DDoS 攻撃を防ぐために、クラウドインフラストラクチャ（オリジン）に移動します。

## オリジンクローキングのメリットは何ですか？

オリジンクロークは、トラフィックによるトラフィックのバイパスを防ぐように設計されています。 [!DNL Fastly Web Application Firewall] （WAF）と、厳密に定義された **[!DNL Fastly]** > **ロードバランサー** > **インスタンス**. この実装では、すべてのトラフィックは次を通過することが保証されます。 [!DNL Fastly] ロードバランサーに組み込まれた内部 WAF と同様に WAF。

## このオリジンのクローク有効化が行われる理由は何ですか？

この機能は、当初、クラウドインフラストラクチャ上のAdobe Commerceにメリットをもたらすために作成されました。

## プロジェクトでオリジンクロークの有効化をリクエストする必要がありますか？

いいえ。 この機能は、既にすべてのクラウドプロジェクトに実装されている必要があり、2021 年以降にプロビジョニングされたプロジェクトでは、デフォルトで有効になっていました。 ただし、次の方法で、プロジェクトのオリジンクロークを無効にするようにリクエストすることもできます [サポートリクエストの送信](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

## オリジン クロークは発信 IP アドレスを変更しますか？

いいえ、ありません。

## オリジンクロークは REST API に影響を与えますか。

[!DNL Fastly] は API 呼び出しをキャッシュしないので、クライアントは変更で問題ありません。 オリジンクロークは、次のような、オリジンに直接移動するリクエストのみをブロックします。

```php
mywebsite.com.c.abcdefghijkl.ent.magento.cloud
```

この例では、クライアントは URL をに変更した場合でも API をヒットできます ``mywebsite.com``:

```php
mywebsite.com/rest/default/V1/integration/admin/token?username=XXXX&password=XXXXX;
mywebsite.com/rest/default/V1/orders/
mywebsite.com/rest/default/V1/products/
mywebsite.com/rest/default/V1/inventory/source-items
```

## この変更はデプロイメントとダウンタイムに影響しますか？

いいえ、この変更は次のようになります **ではない** デプロイメントとダウンタイムに影響します。

## プロジェクトに複数のステージング環境がある場合、オリジンクロークはすべてのステージング環境に適用されますか？

はい。プロジェクトに複数のステージング環境がある場合、変更はすべてのステージング環境に適用されます。
