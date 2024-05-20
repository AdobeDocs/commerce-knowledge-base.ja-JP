---
title: 「設定」を実行:static-content:deploy の deployed_version.txt の問題
description: この記事では、「setup」の実行時に「deployed_version.txt」が書き込み不可エラーの修正について説明します:static-content:コマンドを手動でデプロイします。
exl-id: 88d8c126-349f-49cd-8f02-2a32e4994521
feature: Deploy, Page Content, SCD
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# 実行 `setup:static-content:deploy` deployed_version.txt の問題

この記事では、次の問題を修正します `deployed_version.txt` を実行中は書き込み不可エラーが発生する `setup:static-content:deploy` コマンドを手動で実行します。

## 問題

クラウドインフラストラクチャに関するAdobe Commerceの推奨事項に従って次を使用する場合 [設定の管理](/help/how-to/general/magento-cloud-reduce-deployment-downtime-with-configuration-management.md) （さらに、デプロイメント中に web サイトのダウンタイムを減らすために、静的アセットの生成をビルドステージに移動します）。を実行すると、次のエラーが発生する場合があります。 `setup:static-content:deploy` 手動コマンド：

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

静的コンテンツのデプロイメントを引き続き実行する場合は、以下でシンボリックリンクを削除します。 `pub/static` ディレクトリに移動し、を実行します。 `setup:static-content:deploy` 再びコマンド：

```
find pub/static/ -maxdepth 1 -type l -delete
```
