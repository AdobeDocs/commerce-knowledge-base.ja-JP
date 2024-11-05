---
title: Commerce管理者にログイン後にエラーが発生する
description: この記事では、リクエストされた URL がこのサーバーで見つからなかったというエラーメッセージが表示される問題の解決策を説明します。
exl-id: f52b383b-87f2-4216-9bf4-e765db31ca6b
feature: Admin Workspace
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Commerce管理者にログイン後にエラーが発生する

この記事では、リクエストされた URL がこのサーバーで見つからなかったというエラーメッセージが表示される問題の解決策を説明します。

## 詳細

リクエストされた URL /magento2index.php/admin/admin/dashboard/index/key/0c81957145a968b697c32a846598dc2e/がこのサーバーに見つかりませんでした。

URL の `magento2` と `index.php` の間にスラッシュ文字がないことに注意してください。

## 解決策

ベース URL が正しくありません。 ベース URL には次の条件があります。

* `http://` または `https://` で開始
* スラッシュ（`/`）で終わる
* `core_config_data` データベーステーブル内の `web/unsecure/base_url` レコードの大文字と小文字を一致させる

有効な値を使用してインストールを再実行します。

## 関連資料

Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
