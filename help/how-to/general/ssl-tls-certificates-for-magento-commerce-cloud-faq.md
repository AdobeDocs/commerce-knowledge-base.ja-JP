---
title: クラウドインフラストラクチャ上のAdobe CommerceのSSL （TLS）証明書
description: この記事では、クラウドインフラストラクチャ上のAdobe Commerce サイトのSSL （TLS）証明書の取得に関する質問に対する簡単な回答を提供します。
exl-id: 5a682d07-e4d7-4e81-a2ad-3232f2d8d9c1
feature: Cloud, Console
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: c4af0798-d497-5e6b-8380-19812c26d00a
    internal-label: Console
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 0%
---
# クラウドインフラストラクチャ上のAdobe CommerceのSSL （TLS）証明書

この記事では、クラウドインフラストラクチャ上のAdobe Commerce サイトのSSL （TLS）証明書の取得に関する質問に対する簡単な回答を提供します。

## Adobeで提供されるSSL/TLS証明書は何ですか？

Adobeは、セキュリティで保護されたHTTPS トラフィックを[!DNL Fastly]から提供するために、Domain-Validated [Let&#39;s Encrypt SSL/TLS証明書](https://letsencrypt.org/)を提供します。 Adobeは、クラウドインフラストラクチャ上のAdobe Commerce Pro プランアーキテクチャ、ステージング、およびAdobe Commerce クラウドインフラストラクチャ上のスタータープランアーキテクチャ環境ごとに1つの証明書を提供し、その環境内のすべてのドメインを保護します。

## 証明書は何をカバーしていますか？

Pro プランアーキテクチャの場合、ステージング環境と実稼動専用環境の両方にSSL証明書が作成されます。 PaaS （Platform-as-a-Service）統合環境以外の各専用環境には、その環境に割り当てられたURLに対してこの証明書が割り当てられます。

スタータープランアーキテクチャとPaaS統合環境の場合、環境でプロビジョニングされ、別の証明書で保護されるデフォルトの技術ドメインがあります。

## 既存の証明書に新しいドメインを追加するには？

[!DNL Fastly]のサービスにドメインを追加するには：

1. DNSでドメインをprod.magentocloud.map.fastly.netに指定し、最大6時間待ちます。
1. [ サポートチケット ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を送信して、このドメインをNginx設定に追加することをリクエストします（以前に行っていない場合）。

## 証明書をリクエストするには？

ケース 1

まだWeb サイトを立ち上げていない場合は、カスタマーテクニカルアドバイザー（CTA）からACME Challenge CNAMEを受け取っている可能性があります。 DNSを実稼動URLにすぐに誘導できず、事前に作成されたSSL証明書を取得する必要がある場合にのみ、ACME チャレンジが必要です。

ケース 2

サイトが既に公開されている場合や、ライブサイトにすぐに使用されるURLを指定できる場合は、ACME CNAMEをリクエストする必要はありません。 必要に応じてURLをAdobe Commerce on cloud infrastructure サイトに追加し、DNSを[!DNL Fastly]に指定すると、HTTP検証が機能し、初めてSSL証明書を作成するか、追加のURLで証明書を更新します。

## 独自のSSL/TLS証明書を使用できますか？

Adobeが提供する[Let&#39;s Encrypt証明書](https://letsencrypt.org/)を使用する代わりに、独自のSSL/TLS証明書を指定できます。

ただし、このプロセスを設定および維持するには、追加の作業が必要です。 まず、web サイトのドメイン名（または共通名）の証明書署名リクエスト（CSR）を生成し、SSL ベンダーに提供してSSL証明書を提供する必要があります。

SSL証明書を取得したら、[Adobe Commerce サポートチケット ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を送信するか、CTAと連携してカスタムホスト証明書をクラウド環境に追加します。

* ドメインが使用されなくなった場合、ドメインは当社のシステムから自動的に消去され、それ以上の操作は必要ありません。
* 既に証明書を所有している場合は、SFTP （SSH File Transfer Protocol）クライアントを使用して、サーバー上のwebにアクセスできないファイルの場所に証明書をアップロードし、サポートチケット ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を送信してファイルのパスを知らせます。[

>[!WARNING]
>
>証明書ファイルを直接チケットにアップロードしないことが重要です。 それ以外の場合、証明書は侵害されたと見なされ、Adobeは新しい証明書をリクエストする必要があります。
>ファイルは、SFTPを介してサーバーに任意のフォルダー（例：`var/ssl`、`/tmp/ssl`など）にアップロードする必要があります。その他の方法（機密データを含まない不変ファイルに対してのみ実行する必要があります）は、リポジトリにファイルをコミットするなど、使用しないでください。

## 証明書の名前

SSL証明書の名前はプライマリ URLにのみ関係し、最初のURLで名前が付けられたプライマリホスト名であり、検証および作成するには一致する必要があります。 いくつかのURLがある場合は、証明書にサブジェクト名の代替エントリとして追加されます。 クラウドインフラストラクチャサイト上の1つのAdobe Commerceを指す複数のURLがある場合、共通の名前URL証明書は1つしかなく、SSLでサイトを保護するためにサブジェクトの代替名が追加されます。

## 証明書の「共通名」フィールドにはどのようなドメインが表示されますか？

証明書に表示されるドメインは、TLS証明書に追加された最初のドメインに過ぎません。このドメインは&#x200B;**Common Name** （**CN**）フィールドに入力され、ブラウザーはこの名前を最初に表示します。 **件名の代替名** （**SAN**） フィールドには、TLS証明書のすべてのDNS名が含まれています。 表示される共通名を変更したり、要求したりする方法はありません。

## ワイルドカード TLS証明書を使用できますか？

ワイルドカード TLS証明書は、カスタム証明書でのみ使用でき、Adobe Commerce Let&#39;s Encrypt証明書では使用できません。 TLS最適化の一環として、Adobeではワイルドカード TLS証明書のサポートを終了します。 AdobeのLet&#39;s Encrypt証明書でワイルドカード証明書を使用し、Adobe Commerceの[!DNL Fastly] コンソールで設定されている販売者を特定し、連絡します。 TLS カバレッジを確保するために、これらのワイルドカード証明書を正確なドメインに置き換えることをお願いします。 ワイルドカード TLS証明書を置き換えるには、[!DNL Fastly] プラグインの[domain セクション ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration#manage-domains)にアクセスしてください。 ここから、正確なドメインを追加し、ワイルドカードを削除できます。 これらの新しいドメインがCDNを経由するには、DNSで[!DNL Fastly]を指定する必要があることに注意してください。 ドメインが追加され、DNSが更新されると、一致する[Let&#39;s Encrypt](https://letsencrypt.org/)証明書がプロビジョニングされます。 ワイルドカードを使用して[!DNL Fastly]を指しているドメインを削除しない場合、Adobeは共有証明書を削除します。 これにより、URL FQDNが設定されておらず、同じURL FQDNがDNSで設定されていない場合、サイトが停止する可能性があります。 したがって、構成されたURLが[!DNL Fastly]を指すDNSでも1対1の一致を持っていることを確認する必要があります。

## ドメインがAdobe Commerceを指さなくなった場合はどうすればよいですか？

ドメインがAdobe Commerceを指していない場合は、[!DNL Fastly]/Adobe Commerce システムからドメインを削除してください。 詳しくは、[!DNL Fastly] [ ドメインの削除](https://docs.fastly.com/en/guides/working-with-domains#deleting-a-domain)を参照してください。 ドメインをAdobe Commerceに指定する必要はありませんが、トップレベルのドメイン TLS証明書が必要かどうかを確認してください。 トップレベルドメインが必要な場合は、DNSを更新してAdobe Commerceを指定してください。 既にAdobe Commerceを指している場合は、[lets-encrypt](https://letsencrypt.org/)を含めるようにCAA レコードを更新します。 これらの手順を実行すると、証明書がカバーする必要なセカンダリ URLでLE証明書が更新されます。&#x200B;

## 関連トピックス

[SSL/TLS証明書のプロビジョニング ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#provision-ssltls-certificates)
