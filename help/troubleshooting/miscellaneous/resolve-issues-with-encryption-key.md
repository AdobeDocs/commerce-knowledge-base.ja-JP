---
title: 暗号化キーに関する問題の解決
description: この記事では、暗号化キーが DB ダンプと一緒に他の環境に移動されないことによって発生する問題を修正する方法について説明します。
exl-id: 34410da0-1bd5-421e-9cd7-d3ee75ad8ed7
feature: Cache, Variables
role: Developer
source-git-commit: bee0263da487399ab07bf9158c4d60ab316d6ea1
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# 暗号化キーに関する問題の解決

この記事では、暗号化キーが DB ダンプと一緒に他の環境に移動されないことによって発生する問題を修正する方法について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x

## 問題

をインポートした後 [データベース ダンプ](/help/how-to/general/create-database-dump-on-cloud.md) 実稼動環境からステージング環境または統合環境に至るまで、保存されたクレジットカード番号が間違って表示されるか、マーチャント資格情報の使用が必要な支払い統合で支払いが失敗します。

## 原因：

クレジットカード番号や加盟店資格情報などの機密データの暗号化に使用される暗号化キーは、データベースには格納されないので、データベースダンプのインポート/エクスポート後に他の環境に転送されません。

## 解決策

ソース環境から暗号化キーをコピーし、宛先環境に追加する必要があります。

暗号化キーをコピーするには：

1. データベース ダンプのソースとなったプロジェクトに SSH で接続します（を参照）。 [環境への SSH](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html) 開発者向けドキュメントを参照してください。
1. 開く `app/etc/env.php` テキストエディター。
1. の値をコピーします `key` （用） `crypt`.

```php
return array ('crypt' =>      array ('key' => '<your encryption key>', ),);
```

宛先プロジェクトのキー値を設定するには：

1. を開きます [クラウドコンソール](https://console.adobecommerce.com) をクリックして、プロジェクトを探します。
1. の値を [暗号化\_キー](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html) （開発者ドキュメントの）変数（「」を参照） [プロジェクトの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html) 開発者向けドキュメントを参照してください。 これにより、デプロイメントプロセスがトリガーされ、 `CRYPT_KEY` はで上書きされます `app/etc/env.php` デプロイメントごとにファイルをアップロードします。

オプションで、で手動で暗号化キーを上書きできます `app/etc/env.php` ファイル：

1. 宛先環境に SSH で接続します。
1. 開く `app/etc/env.php` テキストエディター。
1. コピーしたデータをとして貼り付けます。 `key` の値 `crypt`.
1. 編集済みのを保存 `env.php`.
1. 次を実行して、宛先環境のキャッシュをクリーンアップします `bin/magento cache:clean` または、の下のCommerce管理で確認できます。 **システム** > **ツール** > **キャッシュ管理**.
