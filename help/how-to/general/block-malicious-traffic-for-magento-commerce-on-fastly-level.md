---
title: Fastly レベルでAdobe Commerceの悪意のあるトラフィックをブロック
description: この記事では、Adobe Commerce on cloud infrastructure ストアでDDoS攻撃が発生していると疑われる場合に、悪意のあるトラフィックをブロックするために実行できる手順について説明します。
exl-id: 1a834a0a-753b-432e-9c3b-ef8dd034d294
feature: Cache, Marketing Tools
source-git-commit: 8bde15deccc24c548c20cf5955cbebc45ac1d9a1
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Fastly レベルでAdobe Commerceの悪意のあるトラフィックをブロック

この記事では、悪意のある脅威に対応するだけでなく、ジオグラフィックフィルタリングの方法として、ストアへの不要なトラフィックをブロックする方法について説明します。

Adobe Commerceクラウドインフラストラクチャ（およびFastly CDN）は、DDoS攻撃などの悪意のある脅威に対応して、ストアへのトラフィックを管理するツールを提供します。 さらに、悪意のある意図が検出されない場合でも、特定の国や地域からのリクエストをブロックし、ビジネスポリシー、規制要件、その他の運用ニーズに準拠することができます。

## 影響を受ける製品とバージョン：

* Adobe Commerce on cloud infrastructure 2.3.x

この記事では、悪意のあるIPsや、その国やユーザーエージェントが既に存在していることを前提としています。 Adobe Commerce on cloud infrastructureのユーザーは、通常、Adobe Commerce サポートからこの情報を取得します。 次の節では、この情報に基づいてトラフィックをブロックする手順を説明します。 すべての変更は実稼動環境で行う必要があります。

## 管理パネルへのアクセス

Web サイトがDDoSによって過負荷になっている場合は、Commerce管理者にログインできない可能性があります（この記事で詳しく説明されているすべての手順を実行してください）。

管理者にアクセスするには、[&#x200B; メンテナンスモードを有効または無効にする](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode)の説明に従ってweb サイトをメンテナンスモードにし、IP アドレスをホワイトリストに登録します。 これが完了したら、メンテナンスモードを無効にします。

## IPでトラフィックをブロック

Adobe Commerce オンクラウドインフラストラクチャストアの場合、特定のIP アドレスとサブネットによるトラフィックをブロックする最も効果的な方法は、Commerce管理者にFastlyのACLを追加することです。 以下は、より詳細な手順へのリンクを含む手順です。

1. Commerce管理者で、**Stores** > **Configuration** > **Advanced** > **System** > **Full Page Cache** > **Fastly Configuration**&#x200B;に移動します。
1. [&#x200B; ブロックするIP アドレスまたはサブネットのリストを含む新しいACL](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/ACL.md)を作成します。
1. Adobe Commerce用Fastly\_Cdn モジュールの[&#x200B; ブロッキング &#x200B;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) ガイドの説明に従って、これをACL リストとブロックに追加します。

## 国別のトラフィックをブロック

Adobe Commerce オンクラウドインフラストラクチャストアの場合、国別のトラフィックをブロックする最も効果的な方法は、Commerce管理者にFastlyのACLを追加することです。

1. Commerce管理者で、**Stores** > **Configuration** > **Advanced** > **System** > **Full Page Cache** > **Fastly Configuration**&#x200B;に移動します。
1. 国を選択し、Adobe Commerce用Fastly\_Cdn モジュールの[&#x200B; ブロッキング &#x200B;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) ガイドで説明されているように、ACLを使用してブロッキングを設定します。

## ユーザーエージェントによるトラフィックのブロック

ユーザーエージェントに基づいてブロッキングを確立するには、Fastly設定にカスタム VCL スニペットを追加する必要があります。 これを行うには、次の手順を実行します。

1. Commerce管理者で、**Stores** > **Configuration** > **Advanced** > **System** > **Full Page Cache**&#x200B;に移動します。
1. 次に、**Fastly設定** > **カスタム VCL スニペット**&#x200B;です。
1. Fastly\_Cdn モジュールの[&#x200B; カスタム VCL スニペット &#x200B;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md) ガイドの説明に従って、新しいカスタムスニペットを作成します。 次のコードサンプルを例として使用できます。 このサンプルでは、`AhrefsBot` ユーザーエージェントのトラフィックを許可しません。

```php
name: block_bad_useragents
  type: recv
  priority: 5
  VCL:
  if ( req.http.User-Agent ~ "(AhrefsBot)" ) {
      error 405 "Not allowed";
  }
```

## レート制限（実験的なFastly機能）

Adobe Commerce on cloud infrastructureには、実験的なFastly機能があり、特定のパスとweb クローラーのレート制限を指定できます。 詳しくは、[Fastly モジュールのドキュメント &#x200B;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md)を参照してください。

この機能は、実稼動環境で使用する前に、ステージング環境で広範にテストする必要があります。これは、正規のトラフィックをブロックする可能性があるためです。

## 推奨：robots.txtの更新を検討する

`robots.txt` ファイルを更新すると、特定の検索エンジン、web クローラー、およびロボットが特定のページをクロールするのを防ぐことができます。 クロールしないページの例としては、検索結果ページ、チェックアウト、お客様情報などがあります。 これらのページをクロールしないようにすることで、生成されるリクエストの数を減らすことができます。

`robots.txt`を使用する際には、次の2つの重要な考慮事項があります。

* ロボットは`robots.txt`を無視できます。 特に、セキュリティ上の脆弱性をウェブ上でスキャンするマルウェアのロボットや、迷惑メール送信者が利用するメールアドレスの収集には注意が必要です。
* `robots.txt` ファイルは一般公開されているファイルです。 ロボットが使用したくないサーバーのセクションは誰でも確認できます。

基本的な情報とデフォルトのAdobe Commerce `robots.txt`設定については、開発者向けドキュメントの[Search Engine Robots](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/seo-overview#search-engine-robots)記事をご覧ください。

`robots.txt`に関する一般的な情報と推奨事項については、次を参照してください。

* Google サポートによる[robots.txt](https://developers.google.com/search/docs/advanced/robots/create-robots-txt) ファイルの作成
* [/robots.txt](https://www.robotstxt.org/robotstxt.html)について（robotstxt.org）

開発者やSEOの専門家と協力して、許可したいユーザーエージェントや許可しないユーザーエージェントを決定します。

## 関連トピックス

* [Adobe Commerce on Cloudの製品固有のライセンス条件](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeCommerceCloud-WW-2023v1.pdf)
* Commerce on Cloud ガイドのリクエストをブロックするための[&#x200B; カスタム VCL](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-blocking)
