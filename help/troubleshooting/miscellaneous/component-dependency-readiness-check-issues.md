---
title: コンポーネントの依存関係の準備状況チェックの問題
description: この記事では、コンポーネントの依存関係の競合に関する解決策を提供します。
exl-id: e0865226-2aaf-4bdd-8c28-28f32f38ce0c
feature: Configuration
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%
---
# コンポーネントの依存関係の準備状況チェックの問題

この記事では、コンポーネントの依存関係の競合に関する解決策を提供します。

## コンポーネントの依存関係の競合を解決 {#resolve-component-dependency-conflicts}

次の解決策を示された順序で試すことをお勧めします。

1. [競合する依存関係](#trouble-depend-conflict)
1. [ファイルシステム権限の問題](#trouble-depend-permission)
1. [コンポーネント依存関係チェックのステータスは変更されません](#trouble-depend-state)

### 競合する依存関係 {#trouble-depend-conflict}

コンポーネントの依存関係が競合していることが見つかりました&#x200B;*Composerで、インストールまたは更新するコンポーネントを判断できない場合は、*&#x200B;というメッセージが表示されます。 コンポーネントの依存関係の問題を解決するには、Composerの仕組みを十分に理解している技術者である必要があります。

次に、失敗メッセージの例を示します。

```bash
We found conflicting component dependencies.
 You are trying to update package(s) magento/module-sample-data to 1.0.0-beta
 We've detected conflicts with the following packages:
 - magento/sample-data version 0.74.0-beta15. Please try to update it to one of the following package versions: 0.74.0-beta16, 0.74.0-beta14, 0.74.0-beta13, 0.74.0-beta12, 0.74.0-beta11, 0.74.0-beta10, 0.74.0-beta9, 0.74.0-beta8, 0.74.0-beta7
```

>[!NOTE]
>
>表示されるメッセージは異なる可能性があります。

## ファイルシステム権限の問題 {#trouble-depend-permission}

Adobe Commerce ファイルシステムの所有者が、Adobe Commerce ファイルシステム上のディレクトリに書き込む権限を持っていない場合、次のようなメッセージが表示されます。

```bash
file_put_contents(/var/www/html/magento2/var/composer_home/cache/repo/https---
packagist.org/provider-doctrine$instantiator.json): failed to open stream: Permission denied
```

開発者ドキュメントの記事[所有権と権限の概要](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/file-system/overview)で説明されているように、ファイルシステムの権限を設定してください。

## コンポーネント依存関係チェックのステータスは変更されません {#trouble-depend-state}

場合によっては、問題を修正しても、コンポーネント依存関係チェックのステータスが変更されない場合があります。 その場合、`<magento_root>/var/.update_cronjob_status`および`<magento_root>/var/.setup_cronjob_status`という名前のファイルを削除または名前変更して、コンポーネントマネージャーの実行を再試行できます。

これらのファイルの名前を変更または削除すると、コンポーネントマネージャーはチェックを再度実行します。
