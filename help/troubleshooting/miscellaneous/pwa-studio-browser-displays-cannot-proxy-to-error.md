---
title: PWA Studio：ブラウザーに「Cannot proxy to」エラーが表示される
description: このトピックでは、web ブラウザーに「*プロキシ不可*」と表示され、コンソールに「
exl-id: de689633-34b8-4a25-bbd0-a58742c4d03c
feature: Console
role: Developer
source-git-commit: 8be0c125bb0417e34e016656337506da88796630
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# PWA Studio：ブラウザーに「Cannot proxy to」エラーが表示される

このトピックでは、web ブラウザーに「*プロキシ不可*」と表示され、コンソールに以下が表示される場合の解決策について説明します

```
ENOTFOUND
```

プログレッシブ Web アプリケーション（PWA） Studio for Adobe Commerceの使用時にエラーが発生する。

## 影響を受ける製品とバージョン

* Adobe CommerceのPWA Studio

## 問題

<u> 再現手順 </u>:

* ブラウザーでAdobe Commerce ストアを読み込みます。

<u> 期待される結果 </u>:

* Adobe Commerce ストアは、ブラウザーで通常どおり読み込まれます。

<u> 実際の結果 </u>:

* Web ブラウザーに「*プロキシ不可*」エラーが表示され、コンソールに次のようなエラーが表示されます。

```
    ENOTFOUND
```


## 原因：

NodeJS がAdobe Commerce ストアのホスト名を解決できません。

## 解決策

1. Adobe Commerce ストアが複数の web ブラウザーに読み込まれていることを確認してください。
1. ローカルの DNS サーバーまたは VPN を実行している場合は、ホストファイル（`/etc/hosts` にある）にエントリを追加し、このドメインを手動でマッピングして（[ ホストファイル編集に関する一般的な手順 ](https://linuxize.com/post/how-to-edit-your-hosts-file/)）、NodeJS が解決できるようにします。

## 関連資料

* [PWA Studio for Adobe Commerce ドキュメント ](https://developer.adobe.com/commerce/pwa-studio/)
* [ ツールとライブラリ ](https://developer.adobe.com/commerce/pwa-studio/guides/project/tools-libraries/)
