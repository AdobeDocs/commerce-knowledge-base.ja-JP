---
title: Fastly レベルでAdobe Commerceの悪意のあるトラフィックをブロックする
description: この記事では、クラウドインフラストラクチャストア上のAdobe Commerceで DDoS 攻撃が行われていると思われる場合に、悪意のあるトラフィックをブロックするために実行できる手順について説明します。
exl-id: 1a834a0a-753b-432e-9c3b-ef8dd034d294
feature: Cache, Marketing Tools
source-git-commit: f11c8944b83e294b61d9547aefc9203af344041d
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---

# Fastly レベルでAdobe Commerceの悪意のあるトラフィックをブロックする

この記事では、クラウドインフラストラクチャストア上のAdobe Commerceで DDoS 攻撃が行われていると思われる場合に、悪意のあるトラフィックをブロックするために実行できる手順について説明します。

## 影響を受ける製品とバージョン：

* クラウドインフラストラクチャー 2.3.x 上のAdobe Commerce

この記事では、悪意のある IP や、その国およびユーザーエージェントが既に存在することを前提としています。 クラウドインフラストラクチャー上のAdobe Commerceのユーザーは、通常、この情報をAdobe Commerce サポートから取得します。 次の節では、この情報に基づいてトラフィックをブロックする手順を説明します。 すべての変更は、実稼動環境で行う必要があります。

## 管理パネルへのアクセスの取得

Web サイトが DDoS によって過負荷になっている場合、Commerce管理者にログインできない可能性があります（および、この記事で後述するすべての手順を実行する必要があります）。

管理者にアクセスするには、の説明に従って、Web サイトをメンテナンスモードにします。 [メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html#instgde-cli-maint) そして、IP アドレスを許可リストに登録します。 この操作が完了したら、メンテナンスモードを無効にします。

## IP によるトラフィックのブロック

クラウドインフラストラクチャストア上のAdobe Commerceの場合、特定の IP アドレスおよびサブネットによってトラフィックをブロックする最も効果的な方法は、Commerce Admin に Fastly 用の ACL を追加することです。 次に、詳細な手順へのリンクを含む手順を示します。

1. Commerce Admin で、に移動します。 **ストア** > **設定** > **詳細** > **システム** > **フルページキャッシュ** > **Fastly 設定**.
1. [新しい ACL の作成](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/ACL.md) ブロックする IP アドレスまたはサブネットの一覧が表示されます。
1. の説明に従って、ACL リストおよびブロックに追加します。 [ブロック](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) Adobe Commerce用 Fastly\_Cdn モジュールのガイド。

## 国別のトラフィックをブロック

クラウドインフラストラクチャストア上のAdobe Commerceの場合、国別のトラフィックをブロックする最も効果的な方法は、Commerce Admin に Fastly 用の ACL を追加することです。

1. Commerce Admin で、に移動します。 **ストア** > **設定** > **詳細** > **システム** > **フルページキャッシュ** > **Fastly 設定**.
1. 国を選択し、の説明に従って、ACL を使用してブロッキングを設定します。 [ブロック](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) Adobe Commerce用 Fastly\_Cdn モジュールのガイド。

## ユーザーエージェントによるトラフィックのブロック

ユーザーエージェントに基づいてブロックを確立するには、カスタム VCL スニペットを Fastly 設定に追加する必要があります。 これを行うには、次の手順を実行します。

1. Commerce Admin で、に移動します。 **ストア** > **設定** > **詳細** > **システム** > **フルページキャッシュ**.
1. その後 **Fastly 設定** > **カスタム VCL スニペット**.
1. の説明に従って、新しいカスタムスニペットを作成します。 [カスタム VCL スニペット](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md) fastly\_Cdn モジュールのガイド。 例として、次のコードサンプルを使用できます。 このサンプルでは、 `AhrefsBot` および `SemrushBot` ユーザーエージェント。

```php
name: block_bad_useragents
  type: recv
  priority: 5
  VCL:
  if ( req.http.User-Agent ~ "(AhrefsBot|SemrushBot)" ) {
      error 405 "Not allowed";
  }
```

## レート制限（実験的な Fastly 機能）

クラウドインフラストラクチャ上のAdobe Commerceには、実験的な Fastly 機能があり、特定のパスとクローラーのレート制限を指定できます。 を参照してください [Fastly モジュールのドキュメント](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) を参照してください。

この機能は、実稼動環境で使用する前に、ステージング環境で詳細にテストする必要があります。これは、正当なトラフィックをブロックする可能性があるからです。

## 推奨：robots.txt の更新を検討してください

の更新 `robots.txt` ファイルは、特定の検索エンジン、クローラー、ロボットが特定のページをクロールするのを防ぐのに役立つ可能性があります。 クロールしないページの例としては、検索結果ページ、チェックアウト、顧客情報などがあります。 ロボットがこれらのページをクロールするのを防ぐことは、ロボットが生成するリクエストの数を減らすのに役立ちます。

を使用する際には、次の 2 つの重要な考慮事項があります `robots.txt`:

* ロボットは自分のを無視することができる `robots.txt`. 特に、セキュリティの脆弱性を探して Web をスキャンするマルウェアロボットや、スパムの発信者が使用するメールアドレスの収集には注意を払いません。
* この `robots.txt` ファイルは、公開されているファイルです。 ロボットが使用したくないサーバーのセクションは誰でも確認できます。

基本情報とデフォルトのAdobe Commerce `robots.txt` 設定は [検索エンジンロボット](https://docs.magento.com/m2/ee/user_guide/marketing/search-engine-robots.html) 開発者向けドキュメントの記事。

に関する一般的な情報と推奨事項について `robots.txt`を参照してください。

* [robots.txt の作成](https://developers.google.com/search/docs/advanced/robots/create-robots-txt) ファイル（Google サポート提供）
* [/robots.txtについて](https://www.robotstxt.org/robotstxt.html) by robotstxt.org

開発者や SEO の専門家と協力して、許可するユーザーエージェントまたは許可しないユーザーエージェントを決定します。

## 関連資料

[Adobe Commerce on Cloud の製品固有のライセンス条件](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeCommerceCloud-WW-2023v1.pdf)
