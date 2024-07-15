---
title: Commerce Admin でのキャッシュのパージ中のエラー
description: 「この記事では、Commerce管理者でキャッシュをパージする際に発生するエラーメッセージの原因を特定する方法について説明します。 管理者を使用してキャッシュをパージしようとすると、次のメッセージが表示されます。'
exl-id: aa414e04-bc6d-46bd-b98f-0446b97bda14
feature: Admin Workspace, Cache
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Commerce Admin でのキャッシュのパージ中のエラー

この記事では、Commerce管理者でキャッシュをパージする際に発生するエラーメッセージの原因を特定する方法について説明します。 管理者を使用してキャッシュをパージしようとすると、次のメッセージが表示されます。
*/app/project-id/pub/media/catalog/product/cache/directory/filename」ファイルは削除できません。 警告！unlink （/app/project id/pub/media/catalog/product/cache/directory/filename）：そのようなファイルやディレクトリはありません*

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.7、2.4.0 ～ 2.4.2-p1

## 問題

管理者を使用してキャッシュをパージしようとすると、エラーメッセージが表示されます。

<u> 再現手順：</u>

1. 管理者で、**システム**/**ツール**/**キャッシュ管理** に移動します。
1. 任意のクリア キャッシュ オプションを選択します。

<u> 期待される結果：</u>

Adobe Commerceのキャッシュは正常にフラッシュされました（エラーなし）。

<u> 実際の結果：</u>

「ファイルを削除できません」というエラーが発生します。

## 原因：

エラーは、キャッシュクリーニング操作が開始されてから完了とレポートされるまでの遅延に関連しています。

## 解決策

1. エラーで示されているファイルがサーバーに存在しないことを確認します（キャッシュパージが成功したことを確認します）。

```bash
ls -la pub/media/catalog/product/cache/directory/filename
```

次の出力が表示される場合：

```bash
ls: cannot access 'pub/media/catalog/product/cache/directory/filename/': No such file or directory
```

操作が既に完了しているときに、ファイルをクリアしようとしました。 これはバグではありません。メッセージの同時実行性に関する問題で、時々発生すると予想されています。 トラブルシューティングする問題はない。
ただし、ファイルがまだキャッシュに残っていることが出力で示される場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) する必要があります。

## 関連資料

* 開発者向けドキュメントの [ キャッシュ管理 ](https://docs.magento.com/user-guide/system/cache-management.html)。
