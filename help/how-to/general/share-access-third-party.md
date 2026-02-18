---
title: クラウドインフラストラクチャー上のAdobe Commerceに関するサードパーティテストのヒント
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceの拡張機能で問題が発生した場合に、テスト/検証のためにサードパーティとアクセスを共有するためのオプションについて説明します。
exl-id: e2d80aa9-8b68-48ed-bec5-68e128611a1e
feature: Best Practices, Cloud
source-git-commit: 9e218e3fadbf9941c94d309fcfb6f258d2f4faf2
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceに関するサードパーティテストのヒント

この記事では、クラウドインフラストラクチャー上のAdobe Commerceの拡張機能で問題が発生した場合に、テスト/検証のためにサードパーティとアクセスを共有するためのオプションについて説明します。
サードパーティへのアクセスを提供する方法を決定する際には、内部データのセキュリティに関する適切な手順と要件に従う必要があります。

## 影響を受ける製品とバージョン：

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.0 ～ 2.3.7-p1、2.4.0 ～ 2.4.3

## テストに使用する環境

内部のセキュリティ標準に応じて、ローカル環境でサードパーティのトラブルシューティングを行うように選択することもできます。 問題をローカルで再現できない場合は、クラウド環境へのアクセスを提供することをお勧めします。 これを選択する場合は、必ず社内のセキュリティ標準の範囲内で作業してください。 クラウド環境へのアクセスを提供する場合は、可能な操作と、レプリケーションのみ、コード変更の許可などにどのような承認が必要かについて、サードパーティが明確になっていることを確認します。 これは、実稼動環境で特に重要です。

## サードパーティへのアクセスとデータの提供

* サードパーティベンダーにクラウド環境へのアクセスを提供します。 関連記事：

   * [Adobe Commerce ヘルプセンターユーザーガイド/共有アクセス：お使いのアカウントに他のユーザーがアクセスできるようにする権限を付与します &#x200B;](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guidee#shared-access) 詳しくは、サポートナレッジベースを参照してください。
   * ユーザーガイドの [Commerce アカウントの共有 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/commerce-account/commerce-account-share)。

* データベースダンプを作成します（または、サードパーティベンダーにアクセス権を付与します）。 これは、CLI またはCommerce Admin を使用して実行できます。 この DB ダンプは顧客データを難読化するので、コードや製品 SKU などのみが得られ、専有/顧客データは得られません。 サポートナレッジベースで [Commerce アカウントの共有 ] （/help/how-to/general/create-database-dump-on-cloud.md）を参照してください。
* テストが完了したら、サポートナレッジベースの [Adobe Commerceヘルプセンターユーザーガイド/失効（共有アクセスを削除）の説明に従って &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#revoke-shared-access) クラウド環境への共有アクセスを失効させます。

## ベストプラクティスのテスト

標準的な方法は、ローカル環境でのトラブルシューティングです。 問題をローカルに再現できない場合は、ステージングに移動します。 実稼動環境では、サードパーティによるチェックが必要になる場合があります。 実稼動とステージング環境で問題を再現しようとしているだけで、コードを変更しようとしていないことをサードパーティが認識していることを確認します。また、コードの変更が必要な場合は、まず許可を得る必要があります。

## 関連資料

* サポートナレッジベースの [Adobe Commerceでサードパーティの拡張機能を使用するためのベストプラクティス &#x200B;](https://support.magento.com/hc/en-us/articles/360042361152-Best-Practices-for-using-third-party-extensions-in-Magento)。
