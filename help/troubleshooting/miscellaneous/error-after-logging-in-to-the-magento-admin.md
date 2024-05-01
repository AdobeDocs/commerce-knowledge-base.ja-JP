---
title: Commerce管理者にログイン後にエラーが発生する
description: この記事では、リクエストされた URL がこのサーバーで見つからなかったというエラーメッセージが表示される問題の解決策を説明します。
exl-id: f52b383b-87f2-4216-9bf4-e765db31ca6b
feature: Admin Workspace
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Commerce管理者にログイン後にエラーが発生する

この記事では、リクエストされた URL がこのサーバーで見つからなかったというエラーメッセージが表示される問題の解決策を説明します。

## 詳細

リクエストされた URL /magento2index.php/admin/admin/dashboard/index/key/0c81957145a968b697c32a846598dc2e/がこのサーバーに見つかりませんでした。

間にスラッシュ文字がないことに注意してください `magento2` および `index.php` を URL 内に挿入します。

## 解決策

ベース URL が正しくありません。 ベース URL には次の条件があります。

* 次から開始 `http://` または `https://`
* スラッシュ（ `/` ）
* の大文字と小文字を一致させる `web/unsecure/base_url` のレコード `core_config_data` データベーステーブル

有効な値を使用してインストールを再実行します。
