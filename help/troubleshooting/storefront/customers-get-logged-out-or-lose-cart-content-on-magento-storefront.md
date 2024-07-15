---
title: ユーザーがログアウトされたり、Adobe Commerce ストアフロントで買い物かごのコンテンツが失われたりする
description: この記事では、お客様が支払いまたはその他のサードパーティのサービスからAdobe Commerce ストアにリダイレクトされた後、ストアフロントの買い物かごからログアウトされたアイテムが失われる問題の解決策と回避策を説明します（セッション cookie が失われます）。
exl-id: 9175570c-b06c-4a65-b8ca-7a12ff266afb
feature: Orders, Page Content, Shopping Cart, Storefront
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# ユーザーがログアウトされたり、Adobe Commerce ストアフロントで買い物かごのコンテンツが失われたりする

この記事では、お客様が支払いまたはその他のサードパーティのサービスからAdobe Commerce ストアにリダイレクトされた後、ストアフロントの買い物かごからログアウトされたアイテムが失われる問題の解決策を説明します（セッション cookie が失われます）。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス、[ サポートされているすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)
* クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

<u> 再現手順：</u>

1. 顧客は商品をストアフロントの買い物かごに追加し、チェックアウトに進みます。
1. お客様は、支払い/発送またはその他の情報/サービスのためにサードパーティのサイトにリダイレクトされます。
1. ユーザーはストアにリダイレクトされます。

<u> 実際の結果：</u>

お客様が空の買い物かごまたは空白のページにリダイレクト。

<u> 期待される結果：</u>

お客様は、チェックアウトデータと進行状況を失わずに、成功支払いページ（または他の成功ページ）にリダイレクトされました。

## 原因：

SameSite cookie 属性が *Lax* に設定されているか、指定されていない（*Lax* に設定されていると見なされます）。 `SameSite` = *Lax* を指定すると、`POST` リクエストを介した外部 URL への cookie の転送が無効になります。

## 解決策

この問題を解決するには、サードパーティのサービスプロバイダーに問い合わせて、開発者に cookie パラメーターを設定するための統合の更新をリクエストします。

## 関連資料

[Chrome SameSite の更新 ](https://www.chromestatus.com/feature/5088147346030592)
