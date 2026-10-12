---
title: PWA Studio：ブラウザーに「次にプロキシできません」というエラーが表示される
description: このトピックでは、Web ブラウザーに「*プロキシできません*」と表示され、コンソールに「*」と表示される場合の解決策について説明します。
exl-id: de689633-34b8-4a25-bbd0-a58742c4d03c
feature: Console
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: c4af0798-d497-5e6b-8380-19812c26d00a
    internal-label: Console
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%
---
# PWA Studio：ブラウザーに「次にプロキシできません」というエラーが表示される

このトピックでは、Web ブラウザーに「*プロキシできません*」と表示され、コンソールに「」と「

```
ENOTFOUND
```

Adobe Commerce用プログレッシブ web アプリ（PWA） Studioを使用する際のエラー。

## 影響を受ける製品とバージョン

* PWA Studio for Adobe Commerce

## イシュー

<u>再現する手順</u>:

* ブラウザーにAdobe Commerce ストアを読み込みます。

<u>期待される結果</u>:

* Adobe Commerce ストアは、ブラウザーで通常どおり読み込まれます。

<u>実際の結果</u>:

* Web ブラウザーに「*プロキシできません*」というエラーが表示され、コンソールに次のようなエラーが表示されます。

```
    ENOTFOUND
```


## 原因

NodeJSは、Adobe Commerce ストアのホスト名を解決できません。

## Solution

1. Adobe Commerce ストアが複数のweb ブラウザーで読み込まれていることを確認します。
1. ローカル DNS サーバーまたはVPNを実行している場合は、NodeJSが解決できるように、ホスト ファイル（`/etc/hosts`にある）にエントリを追加し、このドメイン（[ ホストファイル編集に関する一般的な手順](https://linuxize.com/post/how-to-edit-your-hosts-file/)）を手動でマッピングします。

## 関連トピックス

* [PWA Studio for Adobe Commerceのドキュメント](https://developer.adobe.com/commerce/pwa-studio/)
* [ツールとライブラリ](https://developer.adobe.com/commerce/pwa-studio/guides/project/tools-libraries/)
