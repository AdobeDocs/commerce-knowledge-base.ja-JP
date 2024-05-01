---
title: 新しいドメインがデフォルトのドメインにリダイレクトされている
description: この記事では、新しいドメインが既存の環境または別の環境でデフォルトのドメインにリダイレクトされる問題を修正します。
exl-id: 88e9eb3f-9b82-4ca3-aa80-e49f360b3eb9
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 新しいドメインがデフォルトのドメインにリダイレクトされている

この記事では、新しいドメインが既存の環境または別の環境でデフォルトのドメインにリダイレクトされる問題を修正します。

## 影響を受ける製品とバージョン

* cloud pro インフラストラクチャ上のAdobe Commerce（すべてのバージョン）

## 問題

新しいドメインは、現在の環境のデフォルトドメインまたは別の環境のデフォルトドメインにリダイレクトされています。

## 原因：

これは、新しいドメインを追加した後や間違ったドメインを追加した後に変数が更新されない場合に発生します [!DNL Fastly] サービスは環境で設定されています。

## 解決策

1. ドメインが同じ環境内でリダイレクトされる場合は、を設定済みであることを確認します [変数](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html#modify-variables).
1. ドメインが別の環境にリダイレクトされている場合は、正しく設定されているかどうかを確認します [!DNL Fastly] 次のコマンドを実行してサービスを実行します。 `bin/magento fastly:conf:get -s`

>[!NOTE]
>
>次を見つけることができます [!DNL Fastly] API 資格情報：各環境（ステージング/実稼動）にログインし、 `/mnt/shared/fastly_tokens.txt` ファイル。 詳しくは、を参照してください [設定 [!DNL Fastly] サービス](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html) （Commerce on Cloud Infrastructure ガイド）を参照してください。

上記の設定の両方が正しい場合は、サポートチケットを送信します。

## 関連資料

* [新しいドメインの設定のチェックリスト](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/checklist-for-setting-up-a-new-domain.html) サポートナレッジベースで。
