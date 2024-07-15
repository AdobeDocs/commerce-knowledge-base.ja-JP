---
title: カテゴリを非表示にするGraphQL クエリが B2B 共有カタログで機能しない
description: この記事では、B2B 共有カタログ機能がGraphQLのカテゴリクエリで機能せず、カテゴリを非表示にする場合の解決策を説明します。
exl-id: bdafa8d9-b637-409e-86b5-d132bccfe0b8
feature: B2B, Catalog Management, Categories, GraphQL, Customer Service
role: Developer
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# カテゴリを非表示にするGraphQL クエリが B2B 共有カタログで機能しない


## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.4.3

## 問題

GraphQLのカテゴリと `categoryList` クエリでは、共有カタログ内のカテゴリを非表示にするカテゴリ権限が無視されます。 これは、B2B 共有カタログ機能がオンになっている、Adobe Commerce 2.4.3 上のすべてのマーチャントに発生します。

<u> 再現手順 </u>:

前提条件：

これは、Adobe Commerceのバックエンド/管理者でAdobe Commerce API を使用し、B2B 共有カタログ機能をオンにしている、PWAのストアフロントでGraphQL 2.4.3 上のすべてのマーチャントに発生します。

1. 複数のカテゴリ（CAT1,CAT2）を作成します。
1. プライベート共有カタログを作成します。
1. 会社ユーザーを作成して、上記の共有カタログに割り当てます。
1. これらの各カテゴリにいくつかの製品を割り当てます。
1. CAT1 をカスタムカタログに割り当て、CAT2 をカスタムプライベートカタログから割り当て解除します。 これにより、共有カタログからすべての製品が CAT2 から割り当て解除されます。
1. カスタムカタログを保存します。
1. CAT2 のカテゴリ権限を *拒否* ブラウジング カテゴリに設定し、顧客グループを上記のプライベートカタログに設定します。
1. 手順 3 で、会社ユーザーとして `categoryList query` または categories クエリを実行します。

<u> 期待される結果 </u>:

結果には CAT1 のみが表示されます。

<u> 実際の結果 </u>:

共有カタログ内で割り当て済み/未割り当て、またはカテゴリ権限の内容に関係なく、すべてのカテゴリが表示されます。

## 原因：

機能が実装されませんでした。

## 解決策

この問題はバージョン 2.4.4 の範囲で修正される予定です。リリース 2.4.4 より前のソリューションが必要な場合は、マーチャントはカスタムパッチを取得するために [ チケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) する必要があります。

## 関連資料

* サポートナレッジベースの [ ベストプラクティス Adobe Commerceのカテゴリ数の制限 ](https://support.magento.com/hc/en-us/articles/360048176832)。
