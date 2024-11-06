---
title: Cloud 上のAdobe Commerceで MySQL に割り当てる領域を増やす
description: この記事では、クラウドインフラストラクチャー上の Adode Commerceで MySQL に領域を割り当てる方法について説明します。
exl-id: 98501aa0-5ec7-4ea1-8856-13d171ad0be9
feature: Cloud
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Cloud 上のAdobe Commerceで MySQL に割り当てる領域を増やす


## スタータープランと Pro プランの統合でのスペースの割り当て

すべてのスタータープラン環境と Pro プラン [ 統合環境 ](/help/announcements/adobe-commerce-announcements/integration-environment-enhancement-request-pro-and-starter.md) の場合、`mysql: disk:` パラメーターを増やすことで、`.magento/services.yaml` ファイルで MySQL により多くの領域を割り当てることができます。 例：

```yaml
mysql:
    type: mysql:10.0
    disk: 2048
```

詳しくは、[MySQL サービスの設定 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/mysql) の記事を参照してください。

`.magento/services.yaml` ファイルを変更したら、変更内容を適用するために、コミットしてプッシュする必要があります。 プッシュはデプロイメントプロセスをトリガーします。

>[!WARNING]
>
>スタータープランのパーティションは、壊滅的なデータ破損を引き起こす可能性があるので、サイズを小さくしないでください（例えば、30 GB から 20 GB に変更する）。

## Pro プランのステージングまたは実稼動での領域の割り当て

Pro プランのステージング環境または実稼動環境用にこれらの変更を行うには、[ サポートチケット ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#merchant-not-displayed) を作成する必要があります。 ストレージを増やすためにサポートチケットを送信する場合、サポートは、ストレージを適用するパーティション（`/mysql` または `/exports`）の量とパーティションを把握する必要があります。 ストレージの増加リクエストには、Adobeアカウントチームの承認が必要です。アカウントチームは、承認する前に、（注文フォームに従って）ストレージの適切な量を確認します。

## 割り当て容量を減らすことができない（Pro および Starter プラン）

Adobe Commerce サポートでは、パーティション （`/mysql` または `/exports`）を増やすことができますが、パーティションを縮小することはできません。 データが破損するリスクがあるため、パーティションのストレージを減らすことはできません。
これは、スタータープランにも当てはまります。スタータープランでは、割り当てられたスペースを自分で増やすことができます。減らすことは強くお勧めせず、データの壊滅的な破損が発生する可能性があります。
