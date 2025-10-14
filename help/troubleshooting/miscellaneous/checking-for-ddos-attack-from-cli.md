---
title: CLI からの DDoS 攻撃の確認
description: この記事では、サーバの Command Line Interface （CLI; コマンドライン インターフェイス）から Distributed Denial of Service （DDoS；分散型サービス拒否）攻撃をチェックする方法について説明します。
exl-id: dfdef289-cf51-42d7-b3fb-d4d2d3760951
feature: Observability
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# CLI からの DDoS 攻撃の確認

この記事では、サーバの Command Line Interface （CLI; コマンドライン インターフェイス）から Distributed Denial of Service （DDoS；分散型サービス拒否）攻撃をチェックする方法について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce、すべてのバージョン
* Magento Open Source、すべてのバージョン

## 問題

Web サイトは低速で、CLI 以外の分析アプリケーションツールにアクセスして DDoS 攻撃の可能性を確認することはできません。 DDoS 攻撃の症状は、ネットワーク設定、使用しているソフトウェアなどによって大きく異なる場合があります。

ただし、DDoS 攻撃の特定に役立つように特別に設計された分析ソフトウェア製品を利用することをお勧めします。

## 原因：

Web サイトの動作が遅くなる原因としては、サーバーの動作が遅くなる、CPU 使用率が高くなる、スクリプトやコードの設定ミスがある、ハードウェアが安価であるなど、複数の原因が考えられます。 場合によっては、DDoS 攻撃が原因である可能性があります。 DDoS 攻撃をチェックするための基本的なツールは、Adobe Commerceのログと CLI です。

ここでも、DDoS 攻撃を特定するために特別に設計されたソフトウェアを使用すると、調査に非常に役立つことに注意することが重要です。

## ソリューションの手順

1. Adobe Commerceのログを調べて、DDoS 攻撃以外の何かが発生していないかどうかを確認します。 詳しくは、開発者向けドキュメントの次の記事を参照してください。
   * [Adobe CommerceとMagento Open Sourceログの場所 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/enable-logging)
   * [&#x200B; クラウドインフラストラクチャログ上のAdobe Commerceの場所 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/test/log-locations)
1. CLI の使用を開始し、`netstat` のコマンドを使用して現在のすべてのインターネット接続を確認します：`netstat -na`。 サーバーへのアクティブな確立済み接続がすべて表示されます。 この場合、同じ IP アドレスからの接続が多すぎると気付くことがあります。
1. 確立された接続をポート 80 （Web サイトの http ポート）で接続するものだけに絞り込んで、1 つの IP アドレスまたは IP アドレスのグループからの接続数が多すぎるかどうかを並べ替えて認識できるようにするには、次のコマンドを使用します。`netstat -an | grep :80 | sort` ポート 443 の https に対しても、同じコマンドを繰り返すことができます：`netstat -an | grep :443 | sort`。 もう 1 つのオプションは、元のコマンドをポート 80 と 443 の両方に拡張することです。`netstat -an | egrep ":80|:443" | sort`。
1. サーバーでアクティブな `SYNC_REC` が多数発生しているかどうかを確認するには、次のコマンドを使用します。     `netstat -n -p|grep SYN_REC | wc -l`     これは通常 5 未満ですが、DDoS 攻撃でははるかに高くなる可能性がありますが、サーバーによっては、通常の状態である可能性が高い場合もあります。
1. `SYNC_REC` のステータスを送信するすべての IP アドレスを一覧表示するには、コマンド `netstat -n -p | grep SYN_REC | sort -u` を使用します。
1. ステータスを送信する一意の IP アドレスをすべて `SYNC_REC` らに一覧表示するには、コマンド `netstat -n -p | grep SYN_REC | awk ‘{print $5}’ | awk -F: ‘{print $1}’` を使用します。
1. また、`netstat` コマンドを使用して、各 IP アドレスがサーバーに対して行った接続数をカウントし計算することもできます。このコマンドは `netstat -ntu | awk ‘{print $5}’ | cut -d: -f1 | sort | uniq -c | sort -n` です。
1. サーバーに接続されている UDP または TCP プロトコル接続の数を一覧表示するには、コマンド `netstat -anp |grep ‘tcp|udp’ | awk ‘{print $5}’ | cut -d: -f1 | sort | uniq -c | sort -n` を使用します。
1. すべての接続ではなく、確立された接続を確認し、各 IP アドレスの接続数を表示するには、コマンド `netstat -ntu | grep ESTAB | awk ‘{print $5}’ | cut -d: -f1 | sort | uniq -c | sort -nr` を使用します。
1. ポート 80 への IP アドレス別の接続数を表示するには、コマンド `netstat -plan|grep :80|awk {‘print $5’}|cut -d: -f 1|sort|uniq -c|sort -nk 1` を使用します。

実際に DDoS 攻撃を受けているかどうかを判断するために、見つかったデータを適切に分析する担当者がいることを確認します。 上記の手順でサーバ CLI から `netstat` コマンドを使用すると、DDoS 攻撃が発生しているかどうかを分析できますが、DDoS 攻撃を特定するために特別に設計されたソフトウェア分析製品を使用すると、適切な分析とともに、DDoS の脅威を特定する最適なツールとなります。

DDoS 攻撃を受けている場合は、ネットワーク構成や DDoS 攻撃の発生状況に応じて実行できる手順が異なりますが、一般的には、ISP に問い合わせたり、サーバーの新しい IP アドレスを取得したり、DDoS の問題の処理に長けた IT 担当者に問い合わせて、特定の状況を分析しアドバイスしたりすることをお勧めします。

## 開発者向けドキュメントの関連する読み値：

* [DDoS 保護 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/fastly#ddos-protection)
* [CLI コマンドの使用 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/deployment/examples/example-using-cli)
* [Commerce用の Cloud CLI](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview)
