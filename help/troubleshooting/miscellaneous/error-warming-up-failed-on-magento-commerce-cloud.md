---
title: 「エラー：クラウドインフラストラクチャのAdobe Commerceでウォーミングアップに失敗しました」
description: 「この記事では、ページキャッシュがウォーミングアップ中に、次のエラーで失敗した場合の解決策を説明します。」
exl-id: 20a88030-b1c9-4fdc-83c1-f344d44cd2e1
feature: Cache, Cloud, Paas
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# エラー：クラウドインフラストラクチャ上のAdobe Commerceでウォーミングアップに失敗しました

この記事では、ページキャッシュがウォームアップ中で、エラーで失敗した場合の解決策を説明します。

*エラー：ウォーミングアップに失敗しました：`<website link>`*

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [サポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

キャッシュウォームアップに失敗しました。

<u>再現手順</u>:

キャッシュのウォームアップ操作を開始します。

<u>期待される結果</u>:

ページまたはサイト全体の読み込み。

<u>実際の結果</u>:

サイトが利用できないか、応答時間が長すぎます。 *エラー：ウォーミングアップに失敗しました：`<website link>`*

## 原因：

キャッシュウォームアップは、HTTP アクセス制御が有効な場合は機能しません。

## 解決策

アクセス制御が有効になっていないことを確認します。特定のブランチ/環境に移動し、 **設定** アイコンをクリックし、 **HTTP アクセス制御** 設定 – このシナリオではキャッシュウォームアップを行えず、アクセス制御を無効にする必要があります。

## 関連資料

* [Adobe Commerce ユーザーガイド / フルページキャッシュ](https://docs.magento.com/user-guide/system/cache-full-page.html) を参照してください。
* [Adobe Commerceでキャッシュのウォーミングアップとサイトを使用できない](/help/troubleshooting/miscellaneous/cache-warming-up-and-site-unavailable-on-magento.md) サポートナレッジベースで。
