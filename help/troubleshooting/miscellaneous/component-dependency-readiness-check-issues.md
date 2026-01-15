---
title: コンポーネントの依存関係の準備チェックの問題
description: この記事では、コンポーネントの依存関係の競合に対するソリューションを提供します。
exl-id: e0865226-2aaf-4bdd-8c28-28f32f38ce0c
feature: Configuration
role: Developer
source-git-commit: 05297c82b292b8ccc88018c58e991bd3a32d6ffa
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# コンポーネントの依存関係の準備チェックの問題

この記事では、コンポーネントの依存関係の競合に対するソリューションを提供します。

## コンポーネントの依存関係の競合を解決する {#resolve-component-dependency-conflicts}

次の解決策を示された順序で試すことをお勧めします。

1. [競合する依存関係](#trouble-depend-conflict)
1. [ファイルシステム権限の問題](#trouble-depend-permission)
1. [コンポーネントの依存関係チェックのステータスは変更されません](#trouble-depend-state)

### 競合する依存関係 {#trouble-depend-conflict}

インストールまたは更新するコンポーネントを Composer で判断できない場合は、メッセージ *競合するコンポーネントの依存関係が見つかりました* が表示されます。 コンポーネントの依存関係の問題を解決するには、Composer の仕組みを十分に理解している技術担当者である必要があります。

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

Adobe Commerce ファイルシステムの所有者がAdobe Commerce ファイルシステム上のディレクトリに書き込む権限を持っていない場合は、次のようなメッセージが表示されます。

```bash
file_put_contents(/var/www/html/magento2/var/composer_home/cache/repo/https---
packagist.org/provider-doctrine$instantiator.json): failed to open stream: Permission denied
```

アドビの開発者ドキュメントの記事 [&#x200B; 所有権と権限の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/file-system/overview) の説明に従って、ファイルシステムの権限を設定してください。

## コンポーネントの依存関係チェックのステータスは変更されません {#trouble-depend-state}

問題を修正しようとしても、コンポーネントの依存関係チェックのステータスが変更されない場合があります。 その場合、`<magento_root>/var/.update_cronjob_status` および `<magento_root>/var/.setup_cronjob_status` という名前のファイルを削除または名前変更して、コンポーネントマネージャーを再実行できます。

これらのファイルの名前を変更または削除すると、コンポーネントマネージャーで再びチェックが実行されます。
