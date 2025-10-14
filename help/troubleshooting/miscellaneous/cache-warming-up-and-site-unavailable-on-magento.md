---
title: Adobe Commerceでキャッシュのウォーミングアップとサイトを使用できない
description: この記事では、ページキャッシュがウォームアップ中で、デプロイメントが停止したり、サイトが停止したりする場合の解決策を提供します。
exl-id: c91d5c1f-95e6-4240-be98-2acea49ae728
feature: Cache, Variables
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Adobe Commerceでキャッシュのウォーミングアップとサイトを使用できない

この記事では、ページキャッシュがウォームアップ中で、デプロイメントが停止したり、サイトが停止したりする場合の解決策を提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [&#x200B; サポート対象バージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。

## 問題

デプロイ後のフェーズの最後に実行されるキャッシュウォームアップスクリプトは、非常に高い割合でリクエストを送信するので、4 CPU のインスタンスなど、特定のインスタンスでは対処できません。 彼らの鼻は労働者の数を使い果たす。

<u> 再現手順 </u>:

キャッシュのウォームアップ操作を開始します。

<u> 期待される結果 </u>:

ページまたはサイト全体の読み込み。

<u> 実際の結果 </u>:

サイトが利用できないか、応答時間が長すぎます。

## 解決策

キャッシュウォームアップ中の同時接続数を制限します。 これには、キャッシュウォームアップスクリプトが同時に送信できるウォームアップリクエストの数を指定するために、`WARM_UP_CONCURRENCY` のデプロイ後変数を追加する必要があります。 このオプションを設定すると、Adobe Commerceのクラウドインフラストラクチャの負荷を管理するのに役立ちます。 手順については、開発者向けドキュメントの [&#x200B; デプロイ後変数/WARM\_UP\_CONCURRENCY](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-post-deploy#warm_up_concurrency) を参照してください。

## 関連資料

ユーザーガイドの [&#x200B; フルページキャッシュ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/cache-management#full-page-caching)
