---
title: 「PWA Studio：ブラウザーに「Cannot proxy to」エラーが表示される」
description: このトピックでは、web ブラウザーに「*プロキシ不可*」と表示され、コンソールに「
exl-id: de689633-34b8-4a25-bbd0-a58742c4d03c
feature: Console
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# PWA Studio：ブラウザーに「Cannot proxy to」エラーが表示される

このトピックでは、web ブラウザーに「」と表示される場合の解決策について説明します&#x200B;*にプロキシできません*」と表示され、コンソールに

```
ENOTFOUND
```

プログレッシブ web アプリケーション（PWA） Studio for Adobe Commerceの使用時にエラーが発生する。

## 影響を受ける製品とバージョン

* Adobe CommerceのPWA Studio

## 問題

<u>再現手順</u>:

* ブラウザーでAdobe Commerce ストアを読み込みます。

<u>期待される結果</u>:

* Adobe Commerce ストアは、ブラウザーで通常どおり読み込まれます。

<u>実際の結果</u>:

* Web ブラウザーに「」と表示されます&#x200B;*にプロキシできません*「エラーが発生し、コンソールに次のようなエラーが表示されます。

```
    ENOTFOUND
```


## 原因：

NodeJS がAdobe Commerce ストアのホスト名を解決できません。

## 解決策

1. Adobe Commerce ストアが複数の web ブラウザーに読み込まれていることを確認してください。
1. ローカルの DNS サーバーまたは VPN を実行している場合は、次の場所にあるホストファイルにエントリを追加します `/etc/hosts`）を選択し、このドメインを手動でマッピングします（[ホストファイル編集の一般的な手順](https://linuxize.com/post/how-to-edit-your-hosts-file/)）に設定する必要があります。これにより、NodeJS が解決できます。

## 関連資料

* [Adobe Commerce ドキュメントのPWA Studio](https://magento.github.io/pwa-studio/)
* [ツールとライブラリ](https://magento.github.io/pwa-studio/technologies/tools-libraries/)
