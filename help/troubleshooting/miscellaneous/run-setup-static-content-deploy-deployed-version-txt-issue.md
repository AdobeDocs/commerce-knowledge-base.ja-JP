---
title: run 'setup:static-content:deploy' deployed_version.txt issue
description: この記事では、「setup:static-content:deploy」コマンドを手動で実行する際の「deployed_version.txt」が書き込み可能ではないエラーを修正します。
exl-id: 88d8c126-349f-49cd-8f02-2a32e4994521
feature: Deploy, Page Content, SCD
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: 17d326fa-534a-55a5-b46f-8ae1de1e2f75
    internal-label: Page Content
  - id: d05f97c9-0a96-5792-92cf-f66ce7326e3a
    internal-label: SCD
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%
---
# `setup:static-content:deploy` deployed_version.txtの問題を実行

この記事では、`setup:static-content:deploy` コマンドを手動で実行する際の`deployed_version.txt`の書き込み不可エラーの修正について説明します。

## イシュー

Adobe Commerce on cloud infrastructureの推奨事項に従ってConfiguration Managementを使用する場合（およびデプロイメント中にweb サイトのダウンタイムを減らすために静的アセットの生成をビルドステージに移行する場合）、`setup:static-content:deploy` コマンドを手動で実行すると、次のエラーが発生する可能性があります。

```
{{cloud-project-id}}_stg@i:~$ php bin/magento setup:static-content:deploy
Requested languages: en_US
Requested areas: frontend, adminhtml
Requested themes: Magento/blank, Magento/luma, Aheadworks/marketplace, Magento/backend
[Magento\Framework\Exception\FileSystemException]
The path "deployed_version.txt:///app/{{cloud-project-id}}_stg/pub/static/app/{{cloud-project-id}}_stg/pub/static/" is not writable
```

## 原因

ダウンタイムを減らすためにデプロイメントプロセスを最適化し、静的アセットファイルをコピーする代わりにシンボリックリンクを作成しました。 静的アセットが保存される場所は読み取り専用であるため、上記のエラーメッセージが表示されます。

静的コンテンツのデプロイを手動で実行することは強くお勧めしません。すべてのアセットが既に生成されており、手動で実行してもファイル間に違いはありません（テーマファイルも読み取り専用なので、変更できません）。そのため、そのような操作には意味がありません。

## Solution

静的コンテンツのデプロイメントを引き続き実行する場合は、`pub/static` ディレクトリ内のシンボリックリンクを削除し、`setup:static-content:deploy` コマンドを再度実行します。

```
find pub/static/ -maxdepth 1 -type l -delete
```
