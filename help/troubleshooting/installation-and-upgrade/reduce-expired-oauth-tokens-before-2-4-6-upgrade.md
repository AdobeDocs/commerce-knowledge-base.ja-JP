---
title: 2.4.6 へのアップグレード前に、期限切れの「oauth_tokens」を減らす
description: この記事では、「oauth_token」テーブルに多数の「oauth_tokens」が表示され、バージョン 2.4.6 へのアップグレードで長い遅延が発生する可能性がある問題の解決策を説明します。CleanExpiredTokens.php を使用して、「oauth_token」テーブルを減らすことをお勧めします。
feature: Variables, Upgrade
role: Developer
exl-id: 92d1d15a-04da-4ba4-b6b8-5c491af9c4c1
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# 期限切れを減らす `oauth_tokens` 2.4.6 へのアップグレード前

この記事では、が多数表示される問題の解決策を示します `oauth_tokens` が含まれる `oauth_token` 表（バージョン 2.4.6 へのアップグレードで長い遅延が生じる可能性があります）を減らすことをお勧めします `oauth_token` を使用したテーブル [`CleanExpiredTokens.php`](https://github.com/magento/magento2/blob/2.4.5-p2/app/code/Magento/Integration/Cron/CleanExpiredTokens.php) [!DNL cron] 期限切れトークンを削除するジョブ。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.0 ～ 2.4.6、すべてのデプロイメント方法

## 問題

多数の `oauth_tokens` が含まれる `oauth_token` 表（バージョン 2.4.6 へのアップグレードに長い遅延が生じる可能性があります）。

アップグレードプロセスには、セキュリティの追加レイヤーのためにこれらのトークンを暗号化することが含まれており、一度に行われるのは 100 件のレコードのみです。 多数のトークンがある場合、これには数時間かかる場合があります。

多数の削減 `oauth_tokens` が含まれる `oauth_token` 表を使用すると、バージョン 2.4.6 へのアップグレードに長い遅延が生じるのを防ぐことができます。

## 解決策

アップグレードを開始する前に、まず [`CleanExpiredTokens.php`](https://github.com/magento/magento2/blob/2.4.5-p2/app/code/Magento/Integration/Cron/CleanExpiredTokens.php) [!DNL cron] ジョブが実行中です。 サイズを縮小します `oauth_token` 期限切れを削除したテーブル `oauth_tokens` トークン。デフォルトで既に有効になっている必要があります。

を手動でトリガーするには [`CleanExpiredTokens.php`](https://github.com/magento/magento2/blob/2.4.5-p2/app/code/Magento/Integration/Cron/CleanExpiredTokens.php) [!DNL cron] ジョブ、実行：
```bin/magento cron:run --group=default```

## 関連資料

* [サービス > [!DNL OAuth]](https://experienceleague.adobe.com/docs/commerce-admin/config/services/oauth.html) （Commerce設定リファレンスガイド）を参照してください。
* [認証ガイド](https://developer.adobe.com/developer-console/docs/guides/authentication/) Adobe Developer ガイドをご覧ください。
