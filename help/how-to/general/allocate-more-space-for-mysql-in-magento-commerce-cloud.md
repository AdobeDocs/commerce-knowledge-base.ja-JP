---
title: Cloud 上のAdobe Commerceで MySQL に割り当てる領域を増やす
description: この記事では、クラウドインフラストラクチャー上の Adode Commerceで MySQL に領域を割り当てる方法について説明します。
exl-id: 98501aa0-5ec7-4ea1-8856-13d171ad0be9
feature: Cloud
source-git-commit: 83b21845cd306336e1cb193a9541478c8a38eea8
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Cloud 上のAdobe Commerceで MySQL に割り当てる領域を増やす


## スタータープランと Pro プランの統合でのスペースの割り当て

すべてのスタータープラン環境および Pro プランの場合 [統合環境](/help/announcements/adobe-commerce-announcements/integration-environment-enhancement-request-pro-and-starter.md)を選択した場合は、で MySQL 用に割り当てる領域を増やすことができます。 `.magento/services.yaml` ファイル（を増やすことで） `mysql: disk:` パラメーター。 例：

```yaml
mysql:
    type: mysql:10.0
    disk: 2048
```

を参照してください。 [MySQL サービスの設定](https://devdocs.magento.com/guides/v2.3/cloud/project/project-conf-files_services-mysql.html) 参照用の記事。

を変更したら、 `.magento/services.yaml` ファイルを保存します。変更を適用するには、それらをコミットしてプッシュする必要があります。 プッシュはデプロイメントプロセスをトリガーします。

>[!WARNING]
>
>スタータープランのパーティションは、壊滅的なデータ破損を引き起こす可能性があるので、サイズを小さくしないでください（例えば、30 GB から 20 GB に変更する）。

## Pro プランのステージングまたは実稼動での領域の割り当て

Pro プランのステージング環境または実稼動環境用にこれらの変更を行うには、 [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#merchant-not-displayed). ストレージを増やすためにサポートチケットを送信する場合、サポートは、ストレージを適用するパーティションの量とパーティションを把握する必要があります（`/mysql` または `/exports`）に設定します。 ストレージの増加リクエストには、Adobeアカウントチームの承認が必要です。アカウントチームは、承認する前に、（注文フォームに従って）ストレージの適切な量を確認します。

## 割り当て容量を減らすことができない（Pro および Starter プラン）

Adobe Commerce サポートでパーティションを増やすことができます（`/mysql` または `/exports`）を指定します。ただし、パーティションを縮小することはできません。 データが破損するリスクがあるため、パーティションのストレージを減らすことはできません。
これは、スタータープランにも当てはまります。スタータープランでは、割り当てられたスペースを自分で増やすことができます。減らすことは強くお勧めせず、データの壊滅的な破損が発生する可能性があります。
