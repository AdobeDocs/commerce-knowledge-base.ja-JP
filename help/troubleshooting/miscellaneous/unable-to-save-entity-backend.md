---
title: エンティティ Adobe Commerce バックエンドを保存できません
description: この記事では、Adobe Commerce バックエンドでエンティティを保存できない場合の解決策を説明します。 例えば、特定の「cart_price」ルールを編集して保存できない場合などです。
exl-id: e45dc88a-2da0-4524-bd61-6634cfebb169
feature: Admin Workspace, Marketing Tools
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# エンティティ Adobe Commerce バックエンドを保存できません

この記事では、Adobe Commerce バックエンドでエンティティを保存できない場合の解決策を説明します。 例えば、特定の `cart_price` ルールを編集して保存できない場合などです。

## 影響を受ける製品とバージョン

この問題は、最大セッションサイズが設定されている、すべてのAdobe Commerce バージョンに影響する可能性があります。 これは、Magento Open Source 2.3.7-p1 およびAdobeコマース（すべてのデプロイメント方法） 2.4.3 以降に追加されました。


## 問題

ストアを再設定しようとすると、ページが再読み込みされ、変更は保存されません。 メッセージは `var/log/system.log` で確認できます。

*[2021-11-27 00:30:52] report.WARNING: セッション サイズ 418056 が、許可されているセッションの最大サイズ 256000 を超えています。[][]*

<u> 再現手順 </u>:

保存されていないストア設定の例を次に示します。

1. 実稼働/**マーケティング**/**買い物かご価格ルール** のAdobe Commerce ストアで、ルールを選択します。
1. ルールを選択し、「*非アクティブ* に設定して、変更を保存します。

<u> 期待される結果 </u>:

ルールが非アクティブに設定されています。

<u> 実際の結果 </u>:

* メッセージなしでページをリロードします。
* ルールはまだアクティブに設定されています。

## 原因：

この問題は、最大セッションサイズに影響を与えた最近導入された新機能に関連しています。 開発者向けドキュメントの [&#x200B; セッション管理 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/security/security-session-management) を参照してください。

## 解決策

（**ストア**/**設定**/**詳細**/**システム**/**セキュリティ**/最大セッションサイズ）で「最大セッションサイズ」の値を大きくします。

## 関連資料

* ユーザーガイドの [&#x200B; マーケティングメニュー &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/marketing-menu)。
