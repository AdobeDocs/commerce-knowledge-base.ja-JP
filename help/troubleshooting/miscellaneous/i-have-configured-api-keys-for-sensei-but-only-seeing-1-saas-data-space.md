---
title: Adobe AI API キーの設定後、複数のSaaS データスペースを表示できない
description: この記事では、Adobe AIのAPI キーを設定した後に、1つのSaaS データスペースしか表示されない問題に対する解決策を提供します。
exl-id: e13041da-b122-4684-8287-42132931f47a
feature: REST, Saas, Observability
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e0ca0e7a-9738-48d1-b98b-615468ab4aaf
    internal-label: REST API
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%
---
# Adobe AI API キーの設定後、複数のSaaS データスペースを表示できない

Commerce サービス（商品レコメンデーションまたはライブサーチ）やCommerceの支払いサービスなどのAdobe AI サービスのAPI キーを設定すると、Adobe Commerce サービスコネクタに複数のSaaS データスペースが表示されます。 製品の使用権限とデプロイメントタイプに応じて、コネクタには1つのSaaS データスペースのみが表示されます。これは、期待される動作です。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）：すべてのバージョン
* Magento Open Source：すべてのバージョン
* 拡張機能やテクノロジー（Fastly、New Relicなど）、Adobe AI（商品レコメンデーション/ライブサーチ）

## イシュー

Adobe AI API キーを設定すると、1つのSaaS データスペースのみが表示されます。

## 原因

利用可能なSaaS データスペースの数は、Commerce アカウントに関連付けられた製品使用権限と、使用されているサービスの種類によって異なります。

## Solution

一般的に、使用可能なSaaS データスペースの数は、Commerce ライセンスによって異なります。

* Adobe Commerce:1つの実稼動データスペースと2つのテストデータスペース
* Magento Open Source：単一の実稼動データスペースとテスト用データスペースなし

決済サービスの場合、デフォルトの動作は次のとおりです。

* Adobe Commerceの決済サービス（*Cloudまたはオンプレミス*）には、デフォルトで3つのデータスペースがあります。
* 単一の本番データスペース
* ふたつのテストデータスペース
* Magento Open Sourceの決済サービスには、デフォルトで1つのデータスペースがあります

複数のクラウドプロジェクトまたはオンプレミス （*ライブ/プロダクション*）のインストールを所有しているお客様は、サポートリクエストを送信することで、各プロジェクトまたはインスタンスの追加の実稼動およびテストデータスペースをリクエストすることもできます。

Adobe決済サービスをご利用のお客様は、Magento Open Sourceのデータスペースをリクエストすることもできます。 テストデータスペースを追加するには、サポートリクエストを送信する前に、支払いチームに事前承認を依頼してください。

>[!NOTE]
> * 複数の環境で同じSaaS データスペースを同時に使用しないでください。 実稼動またはテスト用のデータスペースが環境全体で再利用される場合、データが混在し、クリーンアップが必要になる可能性があります。
> * Adobe Commerce （*Cloud/On-Prem*）の決済サービスには、デフォルトで3つのデータスペースがあります。
> * Magento Open Sourceの決済サービスには、デフォルトで1つのデータスペースがあります。
> 追加のデータスペースをリクエストするには：
> * Adobe決済サービスをご利用のお客様は、Magento Open Sourceのデータスペースをリクエストできます。 テストデータスペースを取得するには、サポートリクエストを送信する前に、支払いチームに事前承認を依頼してください。
> * 複数のクラウドプロジェクトまたはオンプレミス （*ライブ/プロダクション*）のインストールを所有しているお客様は、サポートリクエストを送信することで、各プロジェクトまたはインスタンスの追加の実稼動およびテストデータスペースをリクエストすることもできます。

## 読み上げ

[SaaS データ空間のプロビジョニング](https://experienceleague.adobe.com/ja/docs/commerce/user-guides/integration-services/saas?lang=en#saas-data-space-provisioning)
