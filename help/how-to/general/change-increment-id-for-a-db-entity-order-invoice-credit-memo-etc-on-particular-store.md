---
title: DB エンティティの増分IDの変更（注文、請求書、クレジットメモなど） 特定の店舗で
description: ここでは、Adobe Commerce データベース（DB）エンティティ（注文、請求書、クレジットメモなど）の増分IDを変更する方法について説明します。 'ALTER TABLE' SQL文を使用した特定のAdobe Commerce ストア。
exl-id: 3704dd97-3639-44dc-9b8b-cf09f0c04e6c
feature: Invoices
source-git-commit: e33d0bf6c857d0d54ec1373db79910d78296b054
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# DB エンティティの増分IDの変更（注文、請求書、クレジットメモなど） 特定の店舗で

ここでは、Adobe Commerce データベース（DB）エンティティ（注文、請求書、クレジットメモなど）の増分IDを変更する方法について説明します。 `ALTER TABLE` SQL ステートメントを使用して、特定のAdobe Commerce ストアで。

>[!NOTE]
>
>この記事では、注文、請求書、クレジットメモなどの増分IDの開始数値を変更する方法についてのみ説明します。
>
>増分ID形式を変更する方法や、カスタム接頭辞/接尾辞を追加する方法（たとえば、ORDER-10000001、MYSTORE-10000001、2A10000001などに10000001を変更する方法については説明しません。
>
>形式をカスタマイズするには、カスタム拡張機能または開発作業が必要です。

## 影響のあるバージョン

* Adobe Commerce オンプレミス：2.x.x
* Adobe Commerce オンクラウドインフラストラクチャ：2.x.x
* MySQL: [ サポートされている任意のバージョン ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements)

## 増分IDを変更する必要がある場合（ケース）

次のような場合、新しいDB エンティティの増分IDを変更する必要が生じる可能性があります。

* ライブサイトでのハードバックアップ復元後
* 一部の注文記録は失われましたが、そのIDは既に現在の加盟店アカウントの支払いゲートウェイ（PayPalなど）で使用されています。 このような場合、支払いゲートウェイは、同じIDの新しい注文の処理を停止し、「請求書IDの重複」エラーを返します

>[!NOTE]
>
>また、PayPalの支払い受取設定で請求書IDごとに複数の支払いを許可することで、PayPalの支払いゲートウェイの問題を修正することもできます。 サポートナレッジベースの「[PayPal ゲートウェイがリクエストを拒否しました – 重複した請求書の問題](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26838)」を参照してください。

## 前提条件のステップ

1. 新しい増分IDを変更する必要があるストアとエンティティを検索します。
1. [MySQL DBに](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql-remote)を接続します。 クラウドインフラストラクチャ上のAdobe Commerceの場合、最初に[SSHで環境に接続する必要があります](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. 次のクエリを使用して、エンティティシーケンステーブルの現在のauto\_increment値を確認します。

```sql
SHOW TABLE STATUS FROM `{database_name}` WHERE `name` LIKE 'sequence_{entity_type}_{store_id}';
```

### 例

*ID=1*&#x200B;のストアで注文の自動増分を確認する場合、テーブル名は次のようになります。

```sql
'sequence_order_1'
```

`auto_increment`列の値が&#x200B;*1234*&#x200B;の場合、*ID=1*&#x200B;の店舗に配置された次の注文には&#x200B;*ID \#100001234*&#x200B;が含まれます。

### 関連ドキュメント

* [開発者向けドキュメントのMySQL データベース接続のリモート設定](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql-remote)を参照してください。

## 増分IDを変更するためのエンティティの更新

次のクエリを使用してエンティティを更新します。

```sql
ALTER TABLE sequence_{entity_type}_{store_id} AUTO_INCREMENT = {new_increment_value};
```

>[!WARNING]
>
>重要：新しい増分値は、現在の増分値よりも大きくする必要があります。

### 例

次のクエリを実行した後：

```sql
ALTER TABLE sequence_order_1 AUTO_INCREMENT = 2000;
```

次に&#x200B;*ID=1*&#x200B;の店舗で注文された注文には、*ID \#100002000*&#x200B;が含まれます。

## 実稼動環境（Cloud）に関するその他の推奨ステップ

クラウドインフラストラクチャ上のAdobe Commerceの実稼働環境で`ALTER TABLE` クエリを実行する前に、次の手順を実行することを強くお勧めします。

* ステージング環境で増分IDを変更する手順をテストします
* 失敗した場合に実稼動DBを復元するDB バックアップを[作成](/help/how-to/general/create-database-dump-on-cloud.md)します

## 関連ドキュメント

* [Cloud](/help/how-to/general/create-database-dump-on-cloud.md)でデータベース ダンプを作成します。サポート情報をご覧ください
* ご利用の環境に[SSHを送信する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)方法については、開発者向けドキュメントをご覧ください
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
