---
title: 「[!DNL Fastly] オリジンクローキングの有効化に関する FAQ」
description: この FAQ では、Adobe Commerce（2021 年  [!DNL Fastly]  既に完全に実装されている）でのオリジンクロークの有効化に関するよくある質問について説明しています。
exl-id: d608abe7-7d64-44ce-bea1-34b201c29113
source-git-commit: 1021a1ab81481f92e850bd49330f1742fe9a21f2
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# [!DNL Fastly] オリジンクローキングの有効化に関するよくある質問

この FAQ では、Adobe Commerce（2021 年現在で完全に実装されている）での [!DNL Fastly] オリジンクロークの有効化に関するよくある質問について説明しています。

## オリジン [!DNL Fastly] クローキングとは何ですか？

オリジンクロークは、クラウドインフラストラクチャ上のAdobe Commerceで [!DNL non-Fastly] トラフィックをブロックできるセキュリティ機能です（DDoS 攻撃を防ぐために、クラウドインフラストラクチャ（オリジン）に移動します）。

## オリジンクローキングのメリットは何ですか？

オリジンクロークは、トラフィックが [!DNL Fastly Web Application Firewall] （WAF）をバイパスし、**[!DNL Fastly]**/**ロードバランサー**/**インスタンス** の厳密に定義されたフローを通じてルーティングするのを防ぐように設計されています。 この実装では、すべてのトラフィックが [!DNL Fastly] WAF と、ロードバランサーに組み込まれた内部 WAF を通過することが保証されます。

## このオリジンのクローク有効化が行われる理由は何ですか？

この機能は、当初、クラウドインフラストラクチャ上のAdobe Commerceにメリットをもたらすために作成されました。

## プロジェクトでオリジンクロークの有効化をリクエストする必要がありますか？

いいえ。 この機能は、既にすべてのクラウドプロジェクトに実装されている必要があり、2021 年以降にプロビジョニングされたプロジェクトでは、デフォルトで有効になっていました。

## オリジン クロークは発信 IP アドレスを変更しますか？

いいえ、ありません。

## オリジンクロークは REST API に影響を与えますか。

[!DNL Fastly] は API 呼び出しをキャッシュしないので、クライアントは変更で正常に動作します。 オリジンクロークは、次のような、オリジンに直接移動するリクエストのみをブロックします。

* 実稼動

```php
mywebsite.com.c.abcdefghijkl.ent.magento.cloud
```

* ステージング

```php
mcstaging2.mywebsite.com.c.abcdefghijkl.dev.ent.magento.cloud
```

* ステージング X

```php
mcstagingX.mywebsite.com.c.abcdefghijkl.X.dev.ent.magento.cloud
```

この例では、クライアントは URL を ``mywebsite.com`` に変更した場合でも API をヒットできます。

```php
mywebsite.com/rest/default/V1/integration/admin/token?username=XXXX&password=XXXXX;
mywebsite.com/rest/default/V1/orders/
mywebsite.com/rest/default/V1/products/
mywebsite.com/rest/default/V1/inventory/source-items
```

## この変更はデプロイメントとダウンタイムに影響しますか？

いいえ、この変更はデプロイメントとダウンタイムに **影響しません**。

## プロジェクトに複数のステージング環境がある場合、オリジンクロークはすべてのステージング環境に適用されますか？

はい。プロジェクトに複数のステージング環境がある場合、変更はすべてのステージング環境に適用されます。
