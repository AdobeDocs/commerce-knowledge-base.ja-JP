---
title: クラウド上のAdobe CommerceでMySQL用の空き容量を増やす
description: この記事では、クラウドインフラストラクチャ上のAdobe CommerceでMySQL用のスペースをより多く割り当てる方法について説明します。
exl-id: 98501aa0-5ec7-4ea1-8856-13d171ad0be9
feature: Cloud
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%
---
# クラウド上のAdobe CommerceでMySQL用の空き容量を増やす


## スタータープランとプロプランの統合にスペースを割り当てる

すべてのスタータープラン環境とPro プラン [統合環境](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27242)の場合、`mysql: disk:` パラメーターを増やすことで、`.magento/services.yaml` ファイルのMySQLに多くの領域を割り当てることができます。 例：

```yaml
mysql:
    type: mysql:10.0
    disk: 2048
```

参照については、[MySQL サービスの設定](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/mysql)の記事を参照してください。

`.magento/services.yaml` ファイルを変更したら、変更を確定してプッシュし、適用する必要があります。 プッシュは、デプロイメントプロセスをトリガーします。

>[!WARNING]
>
>スタータープランのパーティションを小さくしないでください（例えば、30 GBから20 GBに変更する）。これにより、データが破損する可能性があります。

## Pro プランのステージングまたは実稼動環境に領域を割り当てる

Pro プランのステージング環境または実稼動環境でこれらの変更を行うには、[ サポートチケット ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)を作成する必要があります。 ストレージを増やすためにサポートチケットを送信する場合、サポートは、ストレージを適用するパーティション（`/mysql`または`/exports`）の量とパーティションを把握する必要があります。 ストレージの増額をリクエストするには、Adobe アカウントチームの承認が必要です。承認を行う前に、（注文フォームに従って）ストレージの利用可能量を確認してください。

## 割り当て済み領域の削減は利用できません（Pro プランとスタータープラン）

Adobe Commerce サポートでは、パーティション （`/mysql`または`/exports`）を拡張できますが、パーティションを縮小することはできません。 データが破損するリスクがあるため、パーティションのストレージを減らすことができません。
また、割り当てられたスペースを自分で増やすことができます。減らすことは非常に推奨されず、壊滅的なデータ破損につながる可能性があります。
