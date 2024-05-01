---
title: Adobe Commerceでキャッシュのウォーミングアップとサイトを使用できない
description: この記事では、ページキャッシュがウォームアップ中で、デプロイメントが停止したり、サイトが停止したりする場合の解決策を提供します。
exl-id: c91d5c1f-95e6-4240-be98-2acea49ae728
feature: Cache, Variables
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Adobe Commerceでキャッシュのウォーミングアップとサイトを使用できない

この記事では、ページキャッシュがウォームアップ中で、デプロイメントが停止したり、サイトが停止したりする場合の解決策を提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [サポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf).

## 問題

デプロイ後のフェーズの最後に実行されるキャッシュウォームアップスクリプトは、非常に高い割合でリクエストを送信するので、4 CPU のインスタンスなど、特定のインスタンスでは対処できません。 彼らの鼻は労働者の数を使い果たす。

<u>再現手順</u>:

キャッシュのウォームアップ操作を開始します。

<u>期待される結果</u>:

ページまたはサイト全体の読み込み。

<u>実際の結果</u>:

サイトが利用できないか、応答時間が長すぎます。

## 解決策

キャッシュウォームアップ中の同時接続数を制限します。 これには、 `WARM_UP_CONCURRENCY` デプロイ後変数を使用して、キャッシュウォームアップスクリプトが同時に送信できるウォームアップリクエストの数を指定します。 このオプションを設定すると、Adobe Commerceのクラウドインフラストラクチャの負荷を管理するのに役立ちます。 手順については、を参照してください [デプロイ後変数/ WARM\_UP\_CONCURRENCY](https://devdocs.magento.com/cloud/env/variables-post-deploy.html#warm_up_concurrency) 開発者向けドキュメントを参照してください。

## 関連資料

[フルページキャッシュ](https://docs.magento.com/user-guide/system/cache-full-page.html) ユーザーガイドの
