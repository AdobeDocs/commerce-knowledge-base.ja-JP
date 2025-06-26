---
title: 特定の店舗の DB エンティティ （注文、請求書、クレジット メモなど）の増分 ID を変更します
description: この記事では、「ALTER TABLE」 SQL 文を使用して、特定のAdobe Commerce ストアでAdobe Commerce Database （DB）エンティティ（注文、請求書、クレジットメモなど）の増分 ID を変更する方法について説明します。
exl-id: 3704dd97-3639-44dc-9b8b-cf09f0c04e6c
feature: Invoices
source-git-commit: e33d0bf6c857d0d54ec1373db79910d78296b054
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# 特定の店舗の DB エンティティ （注文、請求書、クレジット メモなど）の増分 ID を変更します

この記事では、`ALTER TABLE` SQL 文を使用して、特定のAdobe Commerce ストアでAdobe Commerce Database （DB）エンティティ（注文、請求書、クレジットメモなど）の増分 ID を変更する方法について説明します。

>[!NOTE]
>
>この記事では、注文、請求書、クレジットメモなどの増分 ID の開始数値を変更する方法のみを説明します。
>
>増分 ID 形式を変更する方法や、カスタムのプレフィックス/サフィックス（例えば、10000001 を ORDER-10000001、MYSTORE-10000001、2A10000001 などに変更する方法など）を追加する方法については説明していません
>
>形式をカスタマイズするには、カスタム拡張機能または開発作業が必要になります。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス：2.x.x
* クラウドインフラストラクチャー上のAdobe Commerce:2.x.x
* MySQL：任意の [ サポートされているバージョン ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements)

## ID を増分を変更する必要があるのはいつですか（ケース）

次のような場合は、新しい DB エンティティの増分 ID を変更する必要があります。

* ライブサイトでのハードバックアップの復元後
* 一部の注文記録は失われましたが、その ID は、現在のマーチャントアカウントの支払いゲートウェイ（PayPal など）で既に使用されています。 このような場合、支払いゲートウェイは同じ ID を持つ新しい注文の処理を停止し、「請求書 ID が重複」というエラーを返します

>[!NOTE]
>
>また、PayPal の支払い受け取り環境設定で請求書 ID ごとに複数の支払いを許可することで、PayPal の支払いゲートウェイの問題を修正することもできます。 サポートナレッジベースの [PayPal ゲートウェイの拒否リクエスト – 請求書の重複問題 ](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26838) を参照してください。

## 前提条件の手順

1. 新しい増分 ID を変更する必要があるストアとエンティティを見つけます。
1. MySQL DB に [ 接続 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql-remote) します。 クラウドインフラストラクチャー上のAdobe Commerceの場合、最初に [SSH 経由で環境に接続 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html) する必要があります。
1. 次のクエリを使用して、エンティティシーケンステーブルの現在の auto\_increment 値を確認します。

```sql
SHOW TABLE STATUS FROM `{database_name}` WHERE `name` LIKE 'sequence_{entity_type}_{store_id}';
```

### 例

*ID=1* のストアで注文の自動インクリメントをチェックしている場合、テーブル名は次のようになります。

```sql
'sequence_order_1'
```

`auto_increment` 列の値が *1234* の場合、*ID=1* の店舗での次の注文の *ID \#100001234* になります。

### 関連ドキュメント

* 開発者向けドキュメントの [ リモート MySQL データベース接続の設定 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql-remote)。

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

*ID=1* の店舗で次に行われる注文には、*ID \#100002000* が割り当てられます。

## 実稼動環境（クラウド）での追加の推奨手順

クラウドインフラストラクチャー上のAdobe Commerceの実稼動環境で `ALTER TABLE` クエリを実行する前に、次の手順を実行することを強くお勧めします。

* ステージング環境で増分 ID を変更する手順全体をテストします
* [ 作成 ](/help/how-to/general/create-database-dump-on-cloud.md)：障害発生時に本番 DB をリストアするための DB バックアップ

## 関連ドキュメント

* サポートナレッジベースの [ クラウド上にデータベースダンプを作成する ](/help/how-to/general/create-database-dump-on-cloud.md)
* 開発者向けドキュメントの [ お使いの環境に SSH 接続 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
