---
title: 新しいドメインがデフォルトのドメインにリダイレクトされる
description: この記事では、新しいドメインが既存の環境または別の環境のデフォルトドメインにリダイレクトされる問題を修正します。
exl-id: 88e9eb3f-9b82-4ca3-aa80-e49f360b3eb9
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 新しいドメインがデフォルトのドメインにリダイレクトされる

この記事では、新しいドメインが既存の環境または別の環境のデフォルトドメインにリダイレクトされる問題を修正します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud pro インフラストラクチャ（すべてのバージョン）

## イシュー

新しいドメインは、現在の環境のデフォルトドメインまたは別の環境のデフォルトドメインにリダイレクトされます。

## 原因

新しいドメインを追加した後に変数が更新されないか、環境で誤った[!DNL Fastly] サービスが設定されている場合に発生します。

## Solution

1. ドメインが同じ環境内でリダイレクトされている場合は、[変数](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html#modify-variables)を設定していることを確認してください。
1. ドメインが別の環境にリダイレクトされている場合は、次のコマンドを実行して、正しい[!DNL Fastly] サービスを構成しているかどうかを確認します：`bin/magento fastly:conf:get -s`

>[!NOTE]
>
>各環境（ステージング/実稼動環境）にログインし、`/mnt/shared/fastly_tokens.txt` ファイルを確認すると、[!DNL Fastly] API資格情報を見つけることができます。 詳しくは、「Commerce on Cloud Infrastructure ガイド」の「[configure [!DNL Fastly] services](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html)」を参照してください。

上記の両方の設定が正しい場合は、サポートチケットを送信してください。

## 関連トピックス

* [新しいドメインを設定するためのチェックリスト ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/checklist-for-setting-up-a-new-domain.html) （サポートナレッジベース）。
