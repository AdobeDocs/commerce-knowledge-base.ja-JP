---
title: 「setup:static-content:deploy」 deployed_version.txt 問題を実行する
description: 'この記事では、「setup_deploy」コマンドを手動で実行した場合に、「deployed_version.txt」が書き込み不可エラーに修正され :static-content: す。'
exl-id: 88d8c126-349f-49cd-8f02-2a32e4994521
feature: Deploy, Page Content, SCD
role: Developer
source-git-commit: d7c714cf5b2f9db139440d814af26c12001bb4d9
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# deployed_version.txt 問題 `setup:static-content:deploy` 実行

この記事では、`deployed_version.txt` コマンドを手動で実行した際に `setup:static-content:deploy` 書き込み不可エラーが発生した場合の対処法を示します。

## 問題

Adobe Commerce on cloud infrastructure の推奨事項に従って Configuration Management を使用する（および、デプロイメント中に web サイトのダウンタイムを減らすために静的アセットの生成をビルドステージに移行する）場合、`setup:static-content:deploy` コマンドを手動で実行すると、次のエラーが発生する可能性があります。

```
{{cloud-project-id}}_stg@i:~$ php bin/magento setup:static-content:deploy
Requested languages: en_US
Requested areas: frontend, adminhtml
Requested themes: Magento/blank, Magento/luma, Aheadworks/marketplace, Magento/backend
[Magento\Framework\Exception\FileSystemException]
The path "deployed_version.txt:///app/{{cloud-project-id}}_stg/pub/static/app/{{cloud-project-id}}_stg/pub/static/" is not writable
```

## 原因：

デプロイメントプロセスを最適化してダウンタイムを短縮し、静的アセットファイルをコピーする代わりに静的アセットファイルへのシンボリックリンクを作成しました。 静的アセットが保存される場所は読み取り専用なので、上記のエラーメッセージが表示されます。

静的コンテンツのデプロイを手動で実行することを強くお勧めしません。すべてのアセットが既に生成されており、手動で実行するとファイル間の違いがなくなるからです（テーマファイルも読み取り専用であり、変更することはできません）。そのため、このような操作には意味がありません。

## 解決策

静的コンテンツのデプロイメントを引き続き実行する場合は、`pub/static` ディレクトリ内のシンボリックリンクを削除し、`setup:static-content:deploy` コマンドを再度実行します。

```
find pub/static/ -maxdepth 1 -type l -delete
```
