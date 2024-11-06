---
title: クラウドインフラストラクチャー上のAdobe Commerceに対する SSL （TLS）証明書
description: この記事では、アドビのクラウドインフラストラクチャでAdobe Commerce サイトの SSL （TLS）証明書を取得する方法に関する質問に対する回答を示します。
exl-id: 5a682d07-e4d7-4e81-a2ad-3232f2d8d9c1
feature: Cloud, Console
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceに対する SSL （TLS）証明書

この記事では、アドビのクラウドインフラストラクチャでAdobe Commerce サイトの SSL （TLS）証明書を取得する方法に関する質問に対する回答を示します。

## Adobeが提供する SSL/TLS 証明書は何ですか？

Adobeは、ドメイン検証済みの [SSL/TLS 証明書を暗号化しましょう ](https://letsencrypt.org/) 証明書を提供して、[!DNL Fastly] から安全な HTTPS トラフィックを提供します。 Adobeは、クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャ、ステージング、クラウドインフラストラクチャー上のAdobe Commerce Starter プランアーキテクチャ環境ごとに 1 つの証明書を提供し、その環境内のすべてのドメインを保護します。

## 証明書には何が含まれますか？

Pro プランアーキテクチャの場合、ステージング専用環境と実稼動専用環境の両方に SSL 証明書が作成されます。 サービスとしてのプラットフォーム（PaaS）統合環境の外部の各専用環境は、その環境に割り当てられた URL に対してこの証明書を持ちます。

スタータープランアーキテクチャおよび PaaS 統合環境の場合、環境にプロビジョニングされ、別の証明書によって保護されるデフォルトのテクニカルドメインがあります。

## 既存の証明書に新しいドメインを追加するにはどうすればよいですか？

ドメインを [!DNL Fastly] のサービスに追加するには：

1. ドメインを DNS でprod.magentocloud.map.fastly.netに指定し、最大 6 時間待ちます。
1. [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) このドメインを Nginx 設定に追加するようにリクエストします（まだ行っていない場合）。

## 証明書をリクエストするにはどうすればよいですか？

ケース 1

まだ web サイトを立ち上げていない場合は、カスタマーテクニカルアドバイザー（CTA）から ACME チャレンジ CNAME を受け取っている可能性があります。 DNS を即座に実稼動 URL に指定できず、事前に作成した SSL 証明書を取得する必要がある場合にのみ、ACME 認証が必要です。

ケース 2

サイトが既に実稼働している場合や、ライブサイトに使用する URL をすぐに指定できる場合は、ACME CNAME をリクエストする必要はありません。 必要に応じて URL をクラウドインフラストラクチャサイトのAdobe Commerceに追加し、DNS を [!DNL Fastly] に指定すると、HTTP 検証が機能し、初めて SSL 証明書を作成するか、追加の URL で証明書を更新します。

## 独自の SSL/TLS 証明書を使用できますか？

Adobeが提供する [ 証明書を暗号化しましょう ](https://letsencrypt.org/) を使用する代わりに、独自の SSL/TLS 証明書を指定できます。

ただし、このプロセスでは、の設定と保守に追加の作業が必要です。 まず、web サイトのドメイン名（または共通名）の証明書署名要求（CSR）を生成し、SSL ベンダーに提供して SSL 証明書を提供する必要があります。

SSL 証明書を取得したら、[Adobe Commerce サポートチケットを送信するか ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)CTAを使用してカスタムのホスト型証明書をクラウド環境に追加します。

* 使用されなくなったドメインは、システムから自動的にパージされ、それ以上のアクションは必要ありません。
* 既に証明書を所有している場合は、SFTP （SSH ファイル転送プロトコル）クライアントを使用してサーバー上の Web でアクセスできないファイルの場所にアップロードし、ファイルパスを知らせます [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

>[!WARNING]
>
>証明書ファイルをチケットに直接アップロードしないことが重要です。 そうしないと、証明書が侵害されたと見なされ、Adobeは新しい証明書をリクエストする必要があります。
>ファイルは SFTP 経由でサーバーにアップロードする必要があります。ファイルをリポジトリにコミットするなど、他の方法は使用しないでください（機密データを含まない不変ファイルに対してのみ実行する必要があります）。

## 証明書の名前

SSL 証明書の名前は、プライマリ URL に関してのみ重要です。これは、最初の URL で名前が付けられたプライマリホスト名であり、検証および作成されるために一致する必要があります。 URL が少ない場合は、サブジェクトの代替名のエントリとして証明書に追加されます。 クラウドインフラストラクチャサイト上の 1 つのAdobe Commerceを指す URL が複数ある場合は、共通名 URL 証明書が 1 つだけ表示されます。その後、サイトを SSL で保護するために、サブジェクトの代替名が追加されます。

## 証明書の「共通名」フィールドには、どのドメインが表示されますか？

証明書に表示されるドメインは、TLS 証明書に追加された最初のドメインに過ぎず、「**共通名** （**CN**）」フィールドに入力され、ブラウザーに最初にこの名前が表示されます。 **サブジェクト代替名** （**SAN**） フィールドには、TLS 証明書のすべての DNS 名が含まれます。 表示された共通名を変更またはリクエストする方法はありません。

## ワイルドカード TLS 証明書を使用できますか？

ワイルドカード TLS 証明書は、カスタム証明書でのみ使用でき、Adobe Commerce Let&#39;s Encrypt 証明書では使用できません。 TLS 最適化の一環として、Adobeはワイルドカード TLS 証明書のサポートを終了します。 Adobeの Let’s Encrypt 証明書でワイルドカード証明書を使用し、Adobe Commerceの [!DNL Fastly] コンソールで設定されているマーチャントを特定して連絡します。 TLS カバレッジを確保するために、これらのワイルドカード証明書を正確なドメインに置き換えてください。 ワイルドカード TLS 証明書を置き換えるには、[!DNL Fastly] プラグインの [ ドメインセクション ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration#manage-domains) にアクセスしてください。 ここから、正確なドメインを追加したり、ワイルドカードを削除したりできます。 これらの新しいドメインが CDN を経由してルーティングされるようにするには、DNS が [!DNL Fastly] を指している必要があることに注意してください。 ドメインを追加し、DNS が更新されると、一致する [ 暗号化しましょう ](https://letsencrypt.org/) 証明書がプロビジョニングされます。 ワイルドカードを使用して [!DNL Fastly] を指しているドメインを削除しない場合、Adobeは共有証明書を削除します。 URL FQDN が設定されておらず、DNS に同じ URL FQDN が設定されている場合は、サイトが停止する可能性があります。 したがって、設定された URL が、[!DNL Fastly] を指す DNS で 1 対 1 の一致も持つことを確認する必要があります。

## ドメインがAdobe Commerceを指さなくなった場合はどうすればよいですか？

ドメインがAdobe Commerceを指していない場合は、[!DNL Fastly]/Adobe Commerce システムから削除してください。 詳しくは、[!DNL Fastly] ドメインの削除 [ を参照 ](https://docs.fastly.com/en/guides/working-with-domains#deleting-a-domain) てください。 ドメインをAdobe Commerceに指定する必要はありませんが、最上位ドメインの TLS 証明書が必要かどうかを確認します。 トップレベルドメインが必要な場合は、Adobe Commerceを指すように DNS を更新してください。 既にAdobe Commerceを指している場合は、[lets-encrypt](https://letsencrypt.org/) を含めるように CAA レコードを更新します。 これらの手順を実行すると、LE 証明書が更新され、証明書がカバーする必要なセカンダリ URL が表示されます&#x200B;

## 関連資料

開発者向けドキュメントの [SSL/TLS 証明書のプロビジョニング ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#provision-ssltls-certificates)
