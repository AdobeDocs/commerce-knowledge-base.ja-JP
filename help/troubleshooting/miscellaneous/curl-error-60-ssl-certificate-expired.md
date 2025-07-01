---
title: 'cURL エラー 60 : SSL 証明書の有効期限が切れました'
description: この記事では、クラウドインフラストラクチャー上の統合ブランチまたはマスターAdobe Commerce ブランチで SSL 証明書の有効期限が切れました。cURL エラー 60 を受け取った後、ブランチが最後にデプロイされた時期を確認する方法を説明します。
exl-id: 74f1db7e-ee2b-4e27-8fcc-fe462a9e72c3
feature: Configuration
role: Developer
source-git-commit: dcaae51408534b82181b268f60905b123e240900
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# cURL エラー 60 : SSL 証明書の有効期限が切れました

この記事では、`cURL error 60` ールを受信した後にブランチが最後にデプロイされた日時（[!DNL Master] またはクラウドインフラストラクチャ上のAdobe Commerceの [!DNL Integration] ブランチで [!DNL SSL certificate] の有効期限が切れたか）を確認する方法を説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 原因：

これらのブランチの [!DNL SSL certificates] は 30 日間のみ有効で、ブランチは 30 日以上再デプロイされていない可能性があります。

エラーは次のようになります。

```cURL
cURL error 60: SSL certificate problem: certificate has expired
```

>[!NOTE]
>
>これらの証明書は、[!DNL Let's Encrypt] や [!DNL DigiCert] など、よく知られた外部の証明機関（CA）によって署名されていません。 これらは、テストおよび開発目的でAdobe プラットフォームによって管理され、証明書を発行するルートを明示的に信頼しない限り、ブラウザーまたは curl でデフォルトで信頼されない可能性があります。

## 解決策

最後にブランチがデプロイされた日時を確認します。 30 日のしきい値を超えた場合は、ブランチを再デプロイします。

最後のデプロイメントが実行された日時を確認する 2 つの方法：

* [ 方法 1:Use [!DNL magento-cloud] CLI](#meth2)。
* [ 方法 2：を開きます  [!DNL Project URL]](#meth3)。

デプロイメントが正常に完了した場合、[!DNL SSL certificate] は自動的に更新されます。

デプロイメントが失敗し、解決に関するサポートが必要な場合は、[ サポートチケットを送信 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) します。

### 方法 1:CLI[!DNL magento-cloud] 使用 {#meth2}

次のコマンドを実行します：`magento-cloud activity:list --type=environment.push`

### 方法 2:[!DNL Project URL] を開く {#meth3}

`https://demo.magento.cloud/#/projects/<project>/environments/<environment>` に移動して、前回のデプロイメントが実行された日時を確認します。

## 関連資料

開発者向けドキュメントでは、

* [Cloud Manager API: SSLCertificates](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/SSLCertificates)
* [Fastly の設定：SSL/TLS 証明書のプロビジョニング ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#provision-ssltls-certificates)

サポートナレッジベースでは、

* [ カスタム SSL 証明書の有効期限に関する情報 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/custom-ssl-certificate-expiration-information.html)
* [ クラウドインフラストラクチャー上のAdobe Commerceの SSL （TLS）証明書 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq.html)
