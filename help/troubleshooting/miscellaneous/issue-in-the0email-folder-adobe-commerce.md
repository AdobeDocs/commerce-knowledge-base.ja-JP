---
title: クラウド上のAdobe Commerceの var/export フォルダー権限の問題
description: この記事では、「var/export/email」フォルダー内のサーバーでのファイル権限の問題が原因で、製品データを書き出すことができない問題の解決策を説明します。 症状としては、製品やカタログのエクスポートがあり、ユーザーインターフェイスでは使用できませんが、SSH を使用すると表示されます。
exl-id: 68120d3b-f5df-43a5-91f6-2ec519cc25ac
feature: Cloud, Communications, Data Import/Export, Paas, Roles/Permissions
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# クラウド上のAdobe Commerceの var/export フォルダー権限の問題

この記事では、のサーバーでのファイル権限の問題が原因で、製品データを書き出すことができない問題の解決策を説明します `var/export/email` フォルダー。 症状としては、製品やカタログのエクスポートがあり、ユーザーインターフェイスでは使用できませんが、SSH を使用すると表示されます。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce, 2.3.0-2.3.7-p2, 2.4.0-2.4.3-p1

## 問題

内のファイルは書き出すことができません `var/export/email` または `var/export/archive` フォルダー。
権限が原因で、デプロイに失敗しました `var/export/email` または `var/export/email/archive` これは、アーカイブフォルダーがメールの下に作成され、書き出しやメールを行うだけで、サブフォルダーを考慮して何かを追加する以外に問題が発生する場合があるからです） `var/export/email/archive`.

<u>再現手順</u>:

管理者で、に移動します。 **システム** > *データ転送* > **Export**.
に保存する CSV ファイルを選択 `var/export/` フォルダー。

<u>期待される結果</u>:

CSV ファイルは表示可能で、書き出すことができます。

<u>実際の結果</u>:

CSV ファイルが表示されない。 また、権限が拒否されたことを示すメッセージも表示されます。 *RecursiveDirectoryIterator::__construct （/app/project id>/var/export/email）: ディレクトリを開けませんでした：権限が拒否されました*

すべての書き出しタイプ（詳細価格、顧客の財務、顧客のメインファイル、顧客の住所）に対して同じメッセージが表示されます。

## 原因：

これは、内に作成されたフォルダーが原因です `/var` これには不完全な権限があります。 `d-wxrwsr-T`. T スティッキービットとは、ユーザーが所有するファイルのみを削除でき、実行可能ファイルが見つからない場合、ディレクトリ内にファイルを作成できないことを意味します。

この問題は、システムがというフォルダーを作成すると発生することがよくあります。 `export`：というフォルダーを格納します。 `email`：というフォルダーを格納します。 `archive`.

ディレクトリにこれらの誤った権限が設定されているかどうかを確認するには、CLI/ターミナルで次のコマンドを実行します。

`ls -ld var/export/`

権限が正しく設定されていない場合の出力は、次のようになります。

`d-wxrwsr-T 3 web web 4096 Aug 15 19:12 var/export/`


## 解決策

これを解決するには、次のコマンドを実行して、フォルダーの権限を 777 に更新してから、すべてのファイルを再帰的に実行します。

```bash
chmod 777 var/export/
chmod 777 var/export/email/
chmod 777 var/export/email/archive/
chmod 777 -R var/export/
```

## 関連資料

* [Export](https://docs.magento.com/user-guide/system/data-export.html) を参照してください。
