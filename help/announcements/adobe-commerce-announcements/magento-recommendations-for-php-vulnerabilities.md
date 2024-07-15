---
title: Adobe Commerce Recommendations for PHP の脆弱性
description: 9 月 3 日、Multi-State Information Sharing and Analysis Center （MS-ISAC）は、任意のコード実行を可能にする複数の脆弱性に関するアラートと、PHP を使用するすべてのサイトが PHP の最新バージョンに早く更新することを推奨しました（[ 完全なアラートはこちらから ] （https://www.cisecurity.org/advisory/multiple-vulnerabilities-in-php-could-allow-for-arbitrary-code-execution_2019-087/））。
exl-id: 0bc7caab-0b89-463a-a7f2-a7c92df9f84e
feature: Compliance, Recommendations
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Adobe Commerce Recommendations for PHP の脆弱性

9 月 3 日、Multi-State Information Sharing and Analysis Center （MS-ISAC）は、任意のコード実行を可能にする複数の脆弱性に関するアラートと、PHP を使用するすべてのサイトを最新バージョンの PHP に更新するよう勧告を発行しました（[ 完全なアラートはこちらから入手できます ](https://www.cisecurity.org/advisory/multiple-vulnerabilities-in-php-could-allow-for-arbitrary-code-execution_2019-087/)）。

>[!WARNING]
>
>クラウドインフラストラクチャー上のAdobe Commerceの場合、インフラストラクチャチームに 48 営業時間前に通知しない限り、実稼動環境にサービスアップグレードをプッシュすることはできません。 実稼動環境のダウンタイムを最小限に抑え、目的の期間内に設定を更新できるインフラストラクチャサポートエンジニアを確保する必要があるので、これが必要になります。 そのため、変更を実稼動環境で行う必要がある [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)48 時間前に、必要なサービスアップグレードの詳細と、アップグレードプロセスを開始する時刻を指定します。

Adobe Commerce サイトの影響と手順については、以下を参照してください。

**Adobe Commerceはクラウド製品でホストされています**

クラウドインフラストラクチャでAdobe Commerceを使用している場合は、いつでもテクノロジーチームと協力してAdobe Commerceを再デプロイし、更新を活用してください\*。 マーチャントは、これらの脆弱性の結果として発生する可能性のある PCI コンプライアンスの問題を回避するために、9 月 30 日（PT）までにこの再デプロイメントを完了することをお勧めします。

この更新用にクラウドサイトを再デプロイする際の追加メモ：

* サイトで PHP バージョン 7.0 を使用している場合、これらのセキュリティアップデートを利用するには、再デプロイする前にサポートされている PHP バージョンにアップグレードする必要があります。
* 2.1.x/2.2.x の場合、PHP のアップグレードに関する詳細は [ こちら ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version.html) を参照してください。

\* *この記事の以前のバージョンとメッセージングは 9 月 19 日（PT）に発表されましたが、チームは予定より早く作業を完了しました。*

**他のすべてのホスティングソリューションのAdobe Commerce**

Adobe Commerceは PHP に依存しているため、Adobe Commerceを使用するすべてのマーチャントが、ホスティングプロバイダーで PHP に必要な更新を確認することをお勧めします。 また、このレビューと更新は 9 月 30 日までに完了することをお勧めします。これにより、今月末にこれらの脆弱性の結果として生じる可能性のある PCI コンプライアンスの問題を回避するためです。

他のホスティングソリューションにおけるAdobe Commerceの追加詳細を以下に示します。

* 7.1 以前の PHP バージョンを使用するAdobe Commerce バージョン 2.0 または 1.x には、公式の PHP パッチはありません。 推奨されるパスは、PHP をサポートされている PHP バージョンにアップグレードすることです。

アラートによると、この脆弱性に対して推奨されるパッチは次のとおりです。

* PHP 7.1: [https://www.php.net/ChangeLog-7.php\#7.1.32](https://www.php.net/ChangeLog-7.php#7.1.32)
* PHP 7.2: [https://www.php.net/ChangeLog-7.php\#7.2.22](https://www.php.net/ChangeLog-7.php#7.2.22)
* PHP 7.3: [https://www.php.net/ChangeLog-7.php\#7.3.9](https://www.php.net/ChangeLog-7.php#7.3.9)

PHP と最新のリリースについて詳しくは、[PHP のサイト ](https://www.php.net/) を参照してください。 また、セキュリティのベストプラクティスに関するご質問や詳細については、アドビの [ セキュリティのベストプラクティスガイド ](https://www.adobe.com/content/dam/cc/en/security/pdfs/Adobe-Magento-Commerce-Best-Practices-Guide.pdf) を参照してください。
