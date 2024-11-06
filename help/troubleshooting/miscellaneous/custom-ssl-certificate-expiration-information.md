---
title: カスタム SSL 証明書の有効期限情報
description: この記事では、Adobeが提供した SSL 証明書でカスタム SSL 証明書が更新された場合の解決策を説明します。
exl-id: cc968bae-f742-449b-b291-bc121ec45935
feature: Support
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# カスタム SSL 証明書の有効期限情報

この記事では、Adobeが提供した SSL 証明書でカスタム SSL 証明書が更新された場合の解決策を説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

Adobe Commerceは、SSL 証明書の有効期限の 30 日前に自動的に更新します。 この自動処理では、置き換える証明書が内部 SSL かカスタムのサードパーティ SSL かがチェックされず、有効期限が検出されると、有効な内部 SSL に置き換えられます。 これにより、サイト上にカスタム証明書を持つことを想定しているサイト所有者やオペレーターが混乱したり、サイトの停止など、他の機能の問題が発生する可能性が生じたりする可能性があります。

<u> 再現手順 </u>

1. Web サイト用にインストールされたカスタム SSL 証明書。
1. 自動処理は、カスタム SSL 証明書の有効期限が 30 日後になることを検出します。
1. Adobe Commerceは、カスタム証明書をアドビの内部証明書で自動的に置き換えます。

<u> 期待される結果 </u>

Adobe Commerceで SSL 証明書の自動更新を実行している場合、カスタム証明書をスキップします。

<u> 実績 </u>

Adobe Commerceは、有効期限から 30 日後に証明書を更新します。

## 解決策

マーチャントが独自のカスタム SSL 証明書を使用することを選択した場合は、証明書の有効期限の 30 日以上前に更新して、Adobe Commerceの内部 SSL 証明書に置き換えられないようにする必要があります。

独自の SSL を内部 SSL に置き換えた場合に、更新した独自の SSL 証明書で置き換える場合は、新しい証明書ファイルをアップロードした場所で [ サポート依頼を送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。 新しい SSL の開始日を含めてください。 この情報を取得したら、新しい SSL 証明書のインストールを進めることができます。

## 関連資料

* [Magento Commerce Cloud用の SSL （TLS）証明書：よくある質問 ](/help/how-to/general/ssl-tls-certificates-for-magento-commerce-cloud-faq.md) アドビのサポートナレッジベースにあります。
* [ コマンドラインツールのリファレンス：magento-cloud 証明書：add](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-reference#certificateadd) を開発者向けドキュメントに記載しています。
* [Launch チェックリスト ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist) 開発者向けドキュメントに記載されています。
* ユーザーガイドの [Site-Wide Analysis Tool](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#step-2-access-site-wide-analysis-tool) にアクセスします。
