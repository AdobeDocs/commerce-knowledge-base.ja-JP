---
title: クラウドインフラストラクチャー上のAdobe CommerceのBlackfireアクセスの削除
description: 2020 年 4 月 11 日（PT）をもって、クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャおよびBlackfireインフラストラクチャー上のAdobe Commerce Starter プランアーキテクチャのサブスクリプションには、クラウドパフォーマンスモニタリングへの無料アクセスが含まれなくなります。  Blackfireアカウントにログインできなくなります。 Blackfire.io から直接ライセンスを購入することで、4 月 11 日（PT）以降もBlackfireを引き続き使用することができます。 この日までにBlackfireから直接ライセンスを購入していないAdobe Commerce マーチャントの場合、Adobeが提供する無料のBlackfireライセンスが無効になります。 これに伴い、プロファイラーツールを使用して新しいレポートを作成する機能は無効になります。 クラウドインフラストラクチャーでホストされている Pro アーキテクチャを使用しているお客様は、New Relic インフラストラクチャーを介してインフラストラクチャーのパフォーマンスを無償でモニタリングできます。
exl-id: bf33c2c6-e9b3-474a-a127-909b51dff92f
feature: Cloud, Paas
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe CommerceのBlackfireアクセスの削除

2020 年 4 月 11 日（PT）をもって、クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャおよびBlackfireインフラストラクチャー上のAdobe Commerce Starter プランアーキテクチャのサブスクリプションには、クラウドパフォーマンスモニタリングへの無料アクセスが含まれなくなります。  Blackfireアカウントにログインできなくなります。 Blackfire.io から直接ライセンスを購入することで、4 月 11 日（PT）以降もBlackfireを引き続き使用することができます。 この日までにBlackfireから直接ライセンスを購入していないAdobe Commerce マーチャントの場合、Adobeが提供する無料のBlackfireライセンスが無効になります。 これに伴い、プロファイラーツールを使用して新しいレポートを作成する機能は無効になります。 クラウドインフラストラクチャーでホストされている Pro アーキテクチャを使用しているお客様は、New Relic インフラストラクチャーを介してインフラストラクチャーのパフォーマンスを無償でモニタリングできます。

**Blackfireを引き続き使用する場合**:

1. Blackfireのライセンスを直接購入する必要があります。
1. 次に、これらを使用してBlackfireを設定します [手順](https://blackfire.io/docs/integrations/paas/magentocloud).
1. インストールで問題が発生した場合は、次の操作を実行できます [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) お問い合わせください。 Blackfireに関するご質問については、Blackfireサポート （）までお問い合わせください。 [support@blackfire.io](mailto:support@blackfire.io).

## デプロイメントの実行時にエラーが発生した場合：

のデプロイメントを実行すると、Blackfire関連のエラーが発生する場合は、次の操作を行います。

1. 設定からBlackfireを削除します。 を編集する `.magento.app.yaml` ファイルを作成し、ランタイムセクションからBlackfireを削除します。

   ```YAML
   ...
   # Enable extensions required by Magento 2
   runtime:
     extensions:
     - redis
     - xsl
     - json
     -**blackfire**
      - imap
   ...
   ```

1. これをローカル開発環境で完了させ、クラウドにプッシュします。

のみ [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) デプロイメントの実行後に次のエラーが表示される場合：

*PHP の警告：PHP Startup: ダイナミックライブラリ「blackfire.so」を読み込めない（試行済：/usr/lib/php/20180731-zts/blackfire.so （/usr/lib/php/20180731-zts/blackfire.so：共有オブジェクトファイルを開けない：そのようなファイルやディレクトリがない）、/usr/lib/php/20180731-zts/blackfire.so.so （/usr/lib/php/20180731-zts/blackfire.so.so：共有オブジェクトファイルを開けない：そのようなファイルやディレクトリがない）） 0 行目の Unknown*

つまり、Blackfireプラグインを更新し、読み込みを停止する必要があります。

**New Relic インフラストラクチャを使用する場合**:

New Relic インフラストラクチャへのアクセス方法については、以下を参照してください。 [New Relicへのアクセス](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/faq/access-new-relic-services.html) サポートナレッジベースで。
