---
title: DB エンティティ （注文、請求書、クレジット メモなど）の増分 ID を変更 特定の店舗で
description: この記事では、Adobe Commerce Database （DB）エンティティ（注文、請求書、クレジットメモなど）の増分 ID を変更する方法について説明します 「ALTER TABLE」 SQL 文を使用して、特定のAdobe Commerce ストアに対して実行します。
exl-id: 3704dd97-3639-44dc-9b8b-cf09f0c04e6c
feature: Invoices
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# DB エンティティ （注文、請求書、クレジット メモなど）の増分 ID を変更 特定の店舗で

この記事では、Adobe Commerce Database （DB）エンティティ（注文、請求書、クレジットメモなど）の増分 ID を変更する方法について説明します を使用している特定のAdobe Commerce ストアで `ALTER TABLE` SQL 文。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス：2.x.x
* クラウドインフラストラクチャー上のAdobe Commerce:2.x.x
* MySQL：任意 [サポート対象バージョン](https://devdocs.magento.com/guides/v2.2/install-gde/system-requirements-tech.html#database)

## ID を増分を変更する必要があるのはいつですか（ケース）

次のような場合は、新しい DB エンティティの増分 ID を変更する必要があります。

* ライブサイトでのハードバックアップの復元後
* 一部の注文記録は失われましたが、その ID は、現在のマーチャントアカウントの支払いゲートウェイ（PayPal など）で既に使用されています。 このような場合、支払いゲートウェイは同じ ID を持つ新しい注文の処理を停止し、「請求書 ID が重複」というエラーを返します

>[!NOTE]
>
>また、PayPal の支払い受け取り環境設定で請求書 ID ごとに複数の支払いを許可することで、PayPal の支払いゲートウェイの問題を修正することもできます。 参照： [PayPal ゲートウェイ拒否リクエスト – 重複する請求書の問題](/help/troubleshooting/payments/paypal-gateway-rejected-request-duplicate-invoice-issue.md) サポートナレッジベースで。

## 前提条件の手順

1. 新しい増分 ID を変更する必要があるストアとエンティティを見つけます。
1. [接続](https://devdocs.magento.com/guides/v2.2/install-gde/prereq/mysql_remote.html) を MySQL DB に追加します。 クラウドインフラストラクチャー上のAdobe Commerceの場合、最初に以下を行う必要があります [環境に SSH で接続する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html).
1. 次のクエリを使用して、エンティティシーケンステーブルの現在の auto\_increment 値を確認します。

```sql
SHOW TABLE STATUS FROM `{database_name}` WHERE `name` LIKE 'sequence_{entity_type}_{store_id}';
```

### 例

でストア上の注文の自動インクリメントをチェックしている場合 *ID=1*&#x200B;の場合、テーブル名は次のようになります。

```sql
'sequence_order_1'
```

の値 `auto_increment` 列： *1234*：次に店舗で行われた注文 *ID=1* 次を持つことになります *ID \#100001234*.

### 関連ドキュメント

* [リモート MySQL データベース接続の設定](https://devdocs.magento.com/guides/v2.2/install-gde/prereq/mysql_remote.html) 開発者向けドキュメントを参照してください。

## 増分 ID を変更するエンティティを更新

次のクエリを使用してエンティティを更新します。

```sql
ALTER TABLE sequence_{entity_type}_{store_id} AUTO_INCREMENT = {new_increment_value};
```

>[!WARNING]
>
>重要：新しい増分値は、現在の値より大きく、小さくすることはできません。

### 例

次のクエリを実行した後：

```sql
ALTER TABLE sequence_order_1 AUTO_INCREMENT = 2000;
```

次に店に出される注文 *ID=1* 次を持つことになります *ID \#100002000*.

## 実稼動環境（クラウド）での追加の推奨手順

実行する前に `ALTER TABLE` クラウドインフラストラクチャ上のAdobe Commerceの実稼動環境でクエリを実行する場合は、次の手順を実行することを強くお勧めします。

* ステージング環境で増分 ID を変更する手順全体をテストします
* [作成](/help/how-to/general/create-database-dump-on-cloud.md) 障害発生時に本番 DB をリストアするための DB バックアップ

## 関連ドキュメント

* [クラウドにデータベースダンプを作成](/help/how-to/general/create-database-dump-on-cloud.md) サポートナレッジベースで。
* [環境に SSH で接続する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html) 開発者向けドキュメントを参照してください。
