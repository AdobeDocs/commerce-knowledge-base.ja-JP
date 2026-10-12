---
title: カスタムサーバーサイドスクリプトがpub メディアディレクトリで実行されない
description: この記事では、クラウドインフラストラクチャ上のAdobe Commerce アプリケーションの「。/pub/media/」ディレクトリに配置されている場合に、カスタムサーバーサイドスクリプトが実行されない場合の修正点を紹介します。 「。/pub/media/」ディレクトリは書き込み可能なので、これは想定されるセキュリティ制限です。 スクリプトを実行可能にするには、「。/app/code/」や「。/pub/」など、書き込み不可のディレクトリにスクリプトを配置します。
exl-id: fcad8a5d-47d6-4729-93a4-2410d7710d69
feature: Media
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%
---
# カスタムサーバーサイドスクリプトがpub メディアディレクトリで実行されない

この記事では、クラウドインフラストラクチャ上のAdobe Commerce アプリケーションの`./pub/media/` ディレクトリに配置されている場合に、カスタムサーバーサイドスクリプトが実行されない場合の修正について説明します。 `./pub/media/` ディレクトリは書き込み可能なので、これは想定されるセキュリティ制限です。 スクリプトを実行可能にするには、`./app/code/`や`./pub/`など、書き込み不可能なディレクトリにスクリプトを配置します。

## 影響のあるバージョン

* Adobe Commerce クラウドインフラストラクチャ：2.1.x以降、StarterおよびPro プランのアーキテクチャ、WingsおよびLegacy アーキテクチャ

## 問題：スクリプトが実行されない

カスタムサーバーサイドスクリプトは、起動時に実行できません。

例えば、エンドユーザー（Adobe Commerce買い物客）がスクリプト（*domain.com/media/directory/script.php*&#x200B;など）を含む`\*.php` ファイルにつながるリンクをクリックすると、スクリプトは実行ではなくダウンロードされます。

## 原因：スクリプト ファイルの場所が正しくありません

この問題は、スクリプトファイルがクラウドインフラストラクチャ上のAdobe Commerce アプリケーションの`./pub/media/` ディレクトリにある場合に発生します。 これは、予期された動作です。セキュリティの制限により、書き込み可能なディレクトリ （`./pub/media/`）のファイルは実行されません。

## 解決策：書き込み不可能なディレクトリにスクリプトを配置する

サーバー側のスクリプトを書き込み不可能なディレクトリ（`./app/code/`や`./pub/`）に保存します

## 関連ドキュメント

* 開発者向けドキュメントの[Cloud for Adobe Commerce/プロジェクト構造/書き込み可能なディレクトリ &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/file-structure#writable-directories)。
