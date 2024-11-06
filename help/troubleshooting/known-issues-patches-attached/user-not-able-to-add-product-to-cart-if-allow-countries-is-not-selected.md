---
title: 「国を許可」で何も選択されていない場合、ユーザーが買い物かごに製品を追加できない
description: この記事では、「国を許可」が選択されていない場合に商品を買い物かごに追加できない、PHP 8.1 を使用した既知のAdobe Commerce 2.4.4 の問題に対するパッチを提供します。
exl-id: d05d1956-de23-496c-9234-c461a3cfdf36
feature: Orders, Products, Shopping Cart
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 「国を許可」で何も選択されていない場合、ユーザーが買い物かごに製品を追加できない

この記事では、「国を許可」が選択されていない場合に商品を買い物かごに追加できない、PHP 8.1 を使用した既知のAdobe Commerce 2.4.4 の問題に対するパッチを提供します。

## 影響を受ける製品とバージョン

Adobe Commerce 2.4.4 と PHP 8.1

## 問題

「国を許可」が選択されていない場合、ユーザーは買い物かごに製品を追加できません。

<u> 再現手順 </u>:

1. Commerce Admin にログインします。
1. **ストア**/**設定**/**一般**/**国オプション** に移動します。
1. **国を許可** フィールドですべてのオプションを選択解除します。
1. 「**設定を保存**」をクリックして、設定を保存します。
1. ストアフロントに移動して、買い物かごに製品を追加してみてください。

<u> 期待される結果：</u>

買い物かごに製品を追加できます。

<u> 実際の結果：</u>

買い物かごに製品を追加することはできません。 次のコンソールエラーが表示されます。

```bash
Failed to load resource: the server responded with a status of 400 (Bad Request)
customer-data.js:87 Uncaught Error: [object Object]
    at Object.<anonymous> (customer-data.js:87:23)
    at fire (jquery.js:3500:50)
    at Object.fireWith [as rejectWith] (jquery.js:3630:29)
    at done (jquery.js:9798:30)
    at XMLHttpRequest.<anonymous> (jquery.js:10057:37)
```

## 原因：

複数選択設定で選択した項目がない場合、Adobe Commerce設定は `null` を取得します。 この設定は、8.1 より前の PHP バージョンで正常に処理された場合に有効になります。しかし、PHP 8.1 では、「[PHP 8.1 の内部関数の nullable でない引数に null を渡すのは非推奨にする」というエラーが原因で正しく動作しません ](https://wiki.php.net/rfc/deprecate_null_to_scalar_internal_arg)

## 解決策

この問題を解決するには、次のパッチを適用します。

[AC-2655_2.4.4.patch.zip](assets/AC-2655_2.4.4.patch.zip)

## パッチの適用方法

手順については、サポートナレッジベースの [Adobe Commerceが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 役に立つリンク

[ クラウドインフラストラクチャー上のAdobe Commerceにカスタムパッチを適用する ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches) については、開発者向けドキュメントを参照してください。
