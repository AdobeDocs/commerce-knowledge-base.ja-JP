---
title: 誤ったファイルをコミットする際のデプロイメントエラー
description: この記事では、追加すべきでないファイルやフォルダーのリポジトリーへの誤ったコミットによって引き起こされるデプロイメントエラーが発生する場合の問題に対する解決策を提供します。
feature: Deploy
role: Developer
exl-id: c795f9d5-7171-4846-b99f-c018f1d2bf12
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%
---
# 誤ったファイルをコミットする際のデプロイメントエラー

この記事では、追加すべきでないファイルやフォルダーのリポジトリーへの誤ったコミットが原因でデプロイメントエラーが発生する場合の問題を修正します。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure （すべてのバージョン）

## イシュー

ファイル/フォルダーのリポジトリーにコミットすると、デプロイメントエラーが発生します。 例えば、次のエラーは、[&#x200B; ビルド フェーズ &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/deploy/process.html#build-phase)中にDBが現在利用できない場合にDBへの接続を試みたことが原因で発生します。

```SQL
SQLSTATE[HY000] [2002] php_network_getaddresses: getaddrinfo for database.i  
          nternal failed: Name or service not known                                    
                                                                                       
        
        In Abstract.php line 124:
                                                                                       
          SQLSTATE[HY000] [2002] php_network_getaddresses: getaddrinfo for database.i  
          nternal failed: Name or service not known                                    
                                                                                       
        
        In Abstract.php line 124:
                                                                                       
          PDO::__construct(): php_network_getaddresses: getaddrinfo for database.inte  
          rnal failed: Name or service not known       
```

## 原因

特定のファイルやフォルダーは、[&#x200B; デプロイメントワークフロー](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/deploy/process.html)で破損するため、リポジトリにコミットしないでください。

## Solution

これらのファイルやフォルダーが存在する場合は、リポジトリから削除します。

* `app/etc/env.php`
* `pub/media/catalog`
* `vendor`
