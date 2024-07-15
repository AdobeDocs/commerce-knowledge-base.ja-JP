---
title: 間違ったファイルをコミットする際のデプロイメントエラー
description: この記事では、追加すべきでないファイルやフォルダーのリポジトリへの誤ったコミットが原因でデプロイメントエラーが発生する場合の問題に対する解決策を説明します。
feature: Deploy
role: Developer
exl-id: c795f9d5-7171-4846-b99f-c018f1d2bf12
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 間違ったファイルをコミットする際のデプロイメントエラー

この記事では、追加すべきでないファイルやフォルダーのリポジトリへの誤ったコミットが原因でデプロイメントエラーが発生する場合の問題を修正します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 問題

ファイルやフォルダーのリポジトリにコミットすると、デプロイメントエラーが発生します。 例えば、次のエラーは、[ ビルドフェーズ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/deploy/process.html#build-phase) 中に DB が現在使用可能でないときに DB に接続しようとすることが原因で発生します。

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

## 原因：

特定のファイルやフォルダーは、[ デプロイメントワークフロー ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/deploy/process.html) で中断を引き起こすので、リポジトリにコミットしないでください。

## 解決策

これらのファイルやフォルダーが存在する場合は、リポジトリから削除します。

* `app/etc/env.php`
* `pub/media/catalog`
* `vendor`
