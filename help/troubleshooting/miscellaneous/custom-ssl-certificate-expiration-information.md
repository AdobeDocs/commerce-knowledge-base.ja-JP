---
title: カスタム SSL証明書の有効期限の情報
description: この記事では、Adobeが提供するSSL証明書でカスタム SSL証明書が更新された場合の解決策を説明します。
exl-id: cc968bae-f742-449b-b291-bc121ec45935
feature: Support
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: a59f76dc-e003-5617-951e-dffa5bd3de81
    internal-label: Support
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%
---
# カスタム SSL証明書の有効期限の情報

この記事では、Adobeが提供するSSL証明書でカスタム SSL証明書が更新された場合の解決策を説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャ上のAdobe Commerce、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## イシュー

Adobe Commerceは、有効期限の30日前にSSL証明書を自動的に更新します。 この自動化により、置き換えられる証明書が内部SSLまたはカスタム サードパーティ SSLであるかどうかが確認されず、有効期限が検出されると、有効な内部SSLに置き換えられます。 これにより、サイト上にカスタム証明書を持つことを期待するサイト所有者およびオペレーターが混乱する可能性があります。また、サイトの停止など、その他の機能上の問題が発生する可能性もあります。

<u>複製する手順</u>

1. Web サイトにインストールされたカスタム SSL証明書。
1. カスタム SSL証明書の有効期限が30日後であることを自動で検出します。
1. Adobe Commerceは、カスタム証明書を内部証明書に自動的に置き換えます。

<u>期待される結果</u>

Adobe Commerceは、SSL証明書の自動更新を実行する際に、カスタム証明書をスキップします。

<u>実際の結果</u>

Adobe Commerceは、有効期限から30日が経過すると、すべての証明書を更新します。

## Solution

加盟店が独自のカスタム SSL証明書を使用する場合は、証明書の有効期限の30日前までに更新して、内部Adobe Commerce SSL証明書に置き換えないようにする必要があります。

カスタム SSLが内部SSLに置き換えられ、更新されたカスタム SSL証明書に置き換える場合は、新しい証明書ファイルをアップロードした場所で[&#x200B; サポートリクエスト &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を送信してください。 新しいSSLの開始日を含めてください。 この情報が得られたら、新しいSSL証明書のインストールを進めることができます。

## 関連トピックス

* Magento Commerce Cloudの[SSL （TLS）証明書：サポートに関するナレッジベースのFAQ](/help/how-to/general/ssl-tls-certificates-for-magento-commerce-cloud-faq.md)
* [&#x200B; コマンドラインツールのリファレンス：magento-cloud証明書:add](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-reference#certificateadd)を開発者向けドキュメントでご覧ください。
* 開発者向けドキュメントの[&#x200B; チェックリストを起動](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/launch/checklist)します。
* ユーザーガイドの[&#x200B; サイト全体の分析ツール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/site-wide-analysis-tool/access#step-2-access-site-wide-analysis-tool)にアクセスします。
