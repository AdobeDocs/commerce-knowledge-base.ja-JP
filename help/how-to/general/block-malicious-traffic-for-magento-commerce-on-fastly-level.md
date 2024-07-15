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

管理者にアクセスするには、[ メンテナンスモードの有効化または無効化 ](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html#instgde-cli-maint) の説明に従って web サイトをメンテナンスモードにし、IP アドレスを許可リストに登録します。 この操作が完了したら、メンテナンスモードを無効にします。

## IP によるトラフィックのブロック

クラウドインフラストラクチャストア上のAdobe Commerceの場合、特定の IP アドレスおよびサブネットによってトラフィックをブロックする最も効果的な方法は、Commerce Admin に Fastly 用の ACL を追加することです。 次に、詳細な手順へのリンクを含む手順を示します。

1. Commerce管理者で、**ストア**/**設定**/**詳細**/**システム**/**フルページキャッシュ**/**Fastly 設定** に移動します。
1. ブロックする IP アドレスまたはサブネットのリストを使用して [ 新しい ACL を作成 ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/ACL.md) します。
1. ACL リストに追加し、Adobe Commerce用の Fastly\_Cdn モジュールの [ ブロッキング ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) ガイドの説明に従ってブロックします。

## 国別のトラフィックをブロック

クラウドインフラストラクチャストア上のAdobe Commerceの場合、国別のトラフィックをブロックする最も効果的な方法は、Commerce Admin に Fastly 用の ACL を追加することです。

1. Commerce管理者で、**ストア**/**設定**/**詳細**/**システム**/**フルページキャッシュ**/**Fastly 設定** に移動します。
1. 国を選択し、Adobe Commerce用の Fastly\_Cdn モジュールの [ ブロッキング ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) ガイドに記載されているように、ACL を使用してブロッキングを設定します。

## ユーザーエージェントによるトラフィックのブロック

ユーザーエージェントに基づいてブロックを確立するには、カスタム VCL スニペットを Fastly 設定に追加する必要があります。 これを行うには、次の手順を実行します。

1. Commerce管理者で、**ストア**/**設定**/**詳細**/**システム**/**フルページキャッシュ** に移動します。
1. 次に **Fastly 設定**/**カスタム VCL スニペット** を選択します。
1. Fastly\_Cdn モジュールの [ カスタム VCL スニペット ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md) ガイドの説明に従って、新しいカスタムスニペットを作成します。 例として、次のコードサンプルを使用できます。 このサンプルでは、`AhrefsBot` および `SemrushBot` ユーザーエージェントのトラフィックが許可されません。

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

クラウドインフラストラクチャ上のAdobe Commerceには、実験的な Fastly 機能があり、特定のパスとクローラーのレート制限を指定できます。 詳しくは、[Fastly モジュールのドキュメント ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) を参照してください。

この機能は、実稼動環境で使用する前に、ステージング環境で詳細にテストする必要があります。これは、正当なトラフィックをブロックする可能性があるからです。

## 推奨：robots.txt の更新を検討してください

`robots.txt` ファイルを更新すると、特定の検索エンジン、クローラー、ロボットが特定のページをクロールするのを防ぐのに役立つ場合があります。 クロールしないページの例としては、検索結果ページ、チェックアウト、顧客情報などがあります。 ロボットがこれらのページをクロールするのを防ぐことは、ロボットが生成するリクエストの数を減らすのに役立ちます。

`robots.txt` を使用する際には、次の 2 つの重要な考慮事項があります。

* ロボットはあなたの `robots.txt` を無視することができます。 特に、セキュリティの脆弱性を探して Web をスキャンするマルウェアロボットや、スパムの発信者が使用するメールアドレスの収集には注意を払いません。
* `robots.txt` ファイルは、公開されているファイルです。 ロボットが使用したくないサーバーのセクションは誰でも確認できます。

Adobe Commerce `robots.txt` の基本設定とデフォルトの設定については、開発者向けドキュメントの [ 検索エンジンロボット ](https://docs.magento.com/m2/ee/user_guide/marketing/search-engine-robots.html) の記事を参照してください。

`robots.txt` に関する一般的な情報と推奨事項については、以下を参照してください。

* Google サポートによる [robots.txt](https://developers.google.com/search/docs/advanced/robots/create-robots-txt) ファイルの作成
* robotstxt.orgによる [/robots.txtについて ](https://www.robotstxt.org/robotstxt.html)

開発者や SEO の専門家と協力して、許可するユーザーエージェントまたは許可しないユーザーエージェントを決定します。

## 関連資料

[Cloud 上のAdobe Commerceの製品固有のライセンス条件 ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeCommerceCloud-WW-2023v1.pdf)
