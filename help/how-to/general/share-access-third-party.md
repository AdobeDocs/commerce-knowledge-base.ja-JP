---
title: Adobe Commerce on cloud infrastructureのサードパーティテストのヒント
description: この記事では、Adobe Commerce on cloud infrastructureの拡張機能に関する問題がある場合に、テストや検証のためにサードパーティとアクセスを共有するためのオプションを提供します。
exl-id: e2d80aa9-8b68-48ed-bec5-68e128611a1e
feature: Best Practices, Cloud
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%
---
# Adobe Commerce on cloud infrastructureのサードパーティテストのヒント

この記事では、Adobe Commerce on cloud infrastructureの拡張機能に関する問題がある場合に、テストや検証のためにサードパーティとアクセスを共有するためのオプションを提供します。
第三者にアクセスを提供する方法を決定する際には、適切な社内データセキュリティ手順と要件に従う必要があります。

## 影響を受ける製品とバージョン：

* Adobe Commerce on cloud infrastructure 2.3.0 - 2.3.7-p1、2.4.0 - 2.4.3

## テストに使用する環境

社内のセキュリティ基準に応じて、ローカル環境でサードパーティ製のトラブルシューティングを行うこともできます。 問題をローカルで再現できない場合は、クラウド環境へのアクセスを提供することをお勧めします。 これを選択する場合は、必ず内部のセキュリティ標準の範囲内で作業してください。 クラウド環境のいずれかにアクセスを提供する場合は、何ができるか、レプリケーションのみやコード変更の許可などのために必要な承認について、サードパーティに明確に伝えるようにします。 これは、実稼動環境では特に重要です。

## 第三者にアクセスとデータの提供

* サードパーティベンダーにクラウド環境へのアクセスを提供します。 関連記事：

  * [Adobe Commerce ヘルプセンターユーザーガイド >共有アクセス：他のユーザーがアカウントにアクセスするための権限を付与する](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#shared-access)。詳しくは、サポートナレッジベースを参照してください。
  * ユーザーガイドの[Commerce アカウントの共有](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/commerce-account/commerce-account-share)。

* データベースダンプを作成します（または、サードパーティベンダーにアクセス権を付与します）。 これは、CLIまたはCommerce管理者を使用して実行できます。 このDB ダンプは顧客データを難読化するので、取得できるのはコードや製品SKUなどだけで、専有/顧客データはありません。 参考までに、サポートナレッジベースの「[Commerce アカウントの共有]」（/help/how-to/general/create-database-dump-on-cloud.md）を使用してください。
* テストが完了したら、サポート ナレッジベースの[Adobe Commerce ヘルプセンターのユーザーガイド/取り消し（共有アクセスを削除） &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#revoke-shared-access)の説明に従って、クラウド環境への共有アクセスを取り消すようにしてください。

## テストのベストプラクティス

標準的な方法は、ローカル環境でのトラブルシューティングです。 問題をローカルで再現できない場合は、ステージングに移動します。 サードパーティは、本番環境での確認が必要な場合があります。 サードパーティが、実稼動環境とステージング環境で問題を再現し、コードの変更を行わないようにするためだけに行われていることを認識していることを確認し、コードを変更する必要がある場合は、まず許可を得る必要があります。

## 関連トピックス

* Adobe Commerceでサードパーティの拡張機能を使用する際の[&#x200B; ベストプラクティス &#x200B;](https://support.magento.com/hc/en-us/articles/360042361152-Best-Practices-for-using-third-party-extensions-in-Magento)をサポートナレッジベースでご覧ください。
