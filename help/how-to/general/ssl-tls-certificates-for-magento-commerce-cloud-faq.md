---
title: クラウドインフラストラクチャー上のAdobe Commerceに対する SSL （TLS）証明書
description: この記事では、アドビのクラウドインフラストラクチャでAdobe Commerce サイトの SSL （TLS）証明書を取得する方法に関する質問に対する回答を示します。
exl-id: 5a682d07-e4d7-4e81-a2ad-3232f2d8d9c1
feature: Cloud, Console
source-git-commit: 43c3e5f95c4b54e235140cd5b3978d3887af5ee1
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceに対する SSL （TLS）証明書

この記事では、アドビのクラウドインフラストラクチャでAdobe Commerce サイトの SSL （TLS）証明書を取得する方法に関する質問に対する回答を示します。

## Adobeが提供する SSL/TLS 証明書は何ですか？

Adobeは、ドメインで検証済みを提供します [SSL/TLS 証明書を暗号化しましょう](https://letsencrypt.org/) から安全な HTTPS トラフィックを提供するには [!DNL Fastly]. Adobeは、クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャ、ステージング、クラウドインフラストラクチャー上のAdobe Commerce Starter プランアーキテクチャ環境ごとに 1 つの証明書を提供し、その環境内のすべてのドメインを保護します。

## 証明書には何が含まれますか？

Pro プランアーキテクチャの場合、ステージング専用環境と実稼動専用環境の両方に SSL 証明書が作成されます。 サービスとしてのプラットフォーム（PaaS）統合環境の外部の各専用環境は、その環境に割り当てられた URL に対してこの証明書を持ちます。

スタータープランアーキテクチャおよび PaaS 統合環境の場合、環境にプロビジョニングされ、別の証明書によって保護されるデフォルトのテクニカルドメインがあります。

## 既存の証明書に新しいドメインを追加するにはどうすればよいですか？

でドメインをサービスに追加します。 [!DNL Fastly]:

1. ドメインを DNS でprod.magentocloud.map.fastly.netに指定し、最大 6 時間待ちます。
1. [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) このドメインを Nginx 設定に追加するリクエスト（まだ行っていない場合）。

## 証明書をリクエストするにはどうすればよいですか？

ケース 1

まだ web サイトを立ち上げていない場合は、カスタマーテクニカルアドバイザー（CTA）から ACME チャレンジ CNAME を受け取っている可能性があります。 DNS を即座に実稼動 URL に指定できず、事前に作成した SSL 証明書を取得する必要がある場合にのみ、ACME 認証が必要です。

ケース 2

サイトが既に実稼働している場合や、ライブサイトに使用する URL をすぐに指定できる場合は、ACME CNAME をリクエストする必要はありません。 必要に応じて URL をクラウドインフラストラクチャサイトのAdobe Commerceに追加し、DNS をに指定したら、 [!DNL Fastly]、HTTP 検証が機能し、初めて SSL 証明書を作成するか、追加の URL で証明書を更新します。

## 独自の SSL/TLS 証明書を使用できますか？

を使用する代わりに、独自の SSL/TLS 証明書を指定できます [証明書を暗号化しましょう](https://letsencrypt.org/) Adobeが提供。

ただし、このプロセスでは、の設定と保守に追加の作業が必要です。 まず、web サイトのドメイン名（または共通名）の証明書署名要求（CSR）を生成し、SSL ベンダーに提供して SSL 証明書を提供する必要があります。

SSL 証明書を取得したら、 [Adobe Commerce サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) または、CTA と協力して、カスタムでホストされる証明書をクラウド環境に追加します。

* 使用されなくなったドメインは、システムから自動的にパージされ、それ以上のアクションは必要ありません。
* 既に証明書を所有している場合は、SFTP （SSH ファイル転送プロトコル）クライアントを使用して、サーバー上の Web でアクセスできないファイルの場所にアップロードし、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) ファイルのパスを知らせる。

>[!WARNING]
>
>証明書ファイルをチケットに直接アップロードしないことが重要です。 そうしないと、証明書が侵害されたと見なされ、Adobeは新しい証明書をリクエストする必要があります。
>ファイルは SFTP 経由でサーバーにアップロードする必要があります。ファイルをリポジトリにコミットするなど、他の方法は使用しないでください（機密データを含まない不変ファイルに対してのみ実行する必要があります）。

## 証明書の名前

SSL 証明書の名前は、プライマリ URL に関してのみ重要です。これは、最初の URL で名前が付けられたプライマリホスト名であり、検証および作成されるために一致する必要があります。 URL が少ない場合は、サブジェクトの代替名のエントリとして証明書に追加されます。 クラウドインフラストラクチャサイト上の 1 つのAdobe Commerceを指す URL が複数ある場合は、共通名 URL 証明書が 1 つだけ表示されます。その後、サイトを SSL で保護するために、サブジェクトの代替名が追加されます。

## 証明書の「共通名」フィールドには、どのドメインが表示されますか？

証明書に表示されるドメインは、TLS 証明書に追加された最初のドメインのみで、に入力されます **共通名** （**CN**）フィールドおよびブラウザーにこの名前が最初に表示されます。 この **件名の代替名** （**SAN**） フィールドには、TLS 証明書のすべての DNS 名が含まれます。 表示された共通名を変更またはリクエストする方法はありません。

## ワイルドカード TLS 証明書を使用できますか？

ワイルドカード TLS 証明書は、カスタム証明書でのみ使用でき、Adobe Commerce Let&#39;s Encrypt 証明書では使用できません。 TLS 最適化の一環として、Adobeはワイルドカード TLS 証明書のサポートを終了します。 Adobeの Let’s Encrypt 証明書でワイルドカード証明書を使用し、 [!DNL Fastly] Adobe Commerceのコンソール。 TLS カバレッジを確保するために、これらのワイルドカード証明書を正確なドメインに置き換えてください。 ワイルドカード TLS 証明書を置き換えるには、次を参照してください： [ドメイン セクション](https://devdocs.magento.com/cloud/cdn/configure-fastly-customize-cache.html#manage-domains) の [!DNL Fastly] プラグイン。 ここから、正確なドメインを追加したり、ワイルドカードを削除したりできます。 DNS はを指す必要があることに注意してください。 [!DNL Fastly] これらの新しいドメインが CDN を経由してルーティングされるようにするには。 ドメインが追加され、DNS が更新されると、次のように一致します [暗号化しましょう](https://letsencrypt.org/) 証明書がプロビジョニングされます。 を指しているドメインを削除しない場合 [!DNL Fastly] ワイルドカードを使用すると、Adobeによって共有証明書が削除されます。 URL FQDN が設定されておらず、DNS に同じ URL FQDN が設定されている場合は、サイトが停止する可能性があります。 したがって、設定された URL の DNS にも 1 対 1 の一致がを指していることを確認する必要があります。 [!DNL Fastly].

## ドメインがAdobe Commerceを指さなくなった場合はどうすればよいですか？

ドメインがAdobe Commerceを指していない場合は、から削除してください。 [!DNL Fastly]/Adobe Commerce システム。 参照： [!DNL Fastly] [ドメインの削除](https://docs.fastly.com/en/guides/working-with-domains#deleting-a-domain) を参照してください。 ドメインをAdobe Commerceに指定する必要はありませんが、最上位ドメインの TLS 証明書が必要かどうかを確認します。 トップレベルドメインが必要な場合は、Adobe Commerceを指すように DNS を更新してください。 既にAdobe Commerceを指している場合は、以下を含めるように CAA レコードを更新します [lets-encrypt](https://letsencrypt.org/). これらの手順を実行すると、LE 証明書が更新され、証明書がカバーする必要なセカンダリ URL が表示されます&#x200B;

## 関連資料

[SSL/TLS 証明書のプロビジョニング](https://devdocs.magento.com/cloud/cdn/configure-fastly.html#provision-ssltls-certificates) 開発者向けドキュメントで
