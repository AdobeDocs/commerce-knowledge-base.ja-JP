---
title: エンティティ Adobe Commerce バックエンドを保存できません
description: この記事では、Adobe Commerce バックエンドでエンティティを保存できない場合の解決策を説明します。 例えば、特定の「cart_price」ルールを編集して保存できない場合などです。
exl-id: e45dc88a-2da0-4524-bd61-6634cfebb169
feature: Admin Workspace, Marketing Tools
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# エンティティ Adobe Commerce バックエンドを保存できません

この記事では、Adobe Commerce バックエンドでエンティティを保存できない場合の解決策を説明します。 例えば、特定のを編集して保存できない場合などです `cart_price` ルール。

## 影響を受ける製品とバージョン

この問題は、最大セッションサイズが設定されている、すべてのAdobe Commerce バージョンに影響する可能性があります。 これは、Magento Open Source 2.3.7-p1 およびAdobeコマース（すべてのデプロイメント方法） 2.4.3 以降に追加されました。


## 問題

ストアを再設定しようとすると、ページが再読み込みされ、変更は保存されません。 メッセージは、次の場所で確認できます `var/log/system.log`:

*[2021-11-27 00:30:52] report.WARNING: セッション サイズ 418056 は、許可されているセッションの最大サイズ 256000 を超えています。 [][]*

<u>再現手順</u>:

保存されていないストア設定の例を次に示します。

1. 実稼働のAdobe Commerce ストアでルールを選択します > **Marketing** > **買い物かご価格ルール**.
1. ルールを選択してに設定します *Inactive* 変更を保存します。

<u>期待される結果</u>:

ルールが非アクティブに設定されています。

<u>実際の結果</u>:

* メッセージなしでページをリロードします。
* ルールはまだアクティブに設定されています。

## 原因：

この問題は、最大セッションサイズに影響を与えた最近導入された新機能に関連しています。 参照： [セッション管理](https://docs.magento.com/user-guide/stores/security-session-management.html) 開発者向けドキュメントを参照してください。

## 解決策

の「最大セッションサイズ」の値を大きくします（**ストア** > **設定** > **詳細** > **システム** > **セキュリティ** > 最大セッションサイズ）。

## 関連資料

* [マーケティングメニュー](https://docs.magento.com/user-guide/marketing/marketing-menu.html) を参照してください。
