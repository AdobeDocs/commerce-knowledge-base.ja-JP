---
title: pub メディアディレクトリで実行されないカスタムサーバーサイドスクリプト
description: この記事では、「」に配置した場合にカスタムのサーバーサイドスクリプトが実行されない問題を修正しました。クラウドインフラストラクチャー上のAdobe Commerce アプリケーションの/pub/media/' ディレクトリ。 「」以来、これは想定されるセキュリティ制限です。/pub/media/' ディレクトリは書き込み可能です。 スクリプトを実行可能にするには、書き込み不可能なディレクトリ（例：）にスクリプトを配置します。/app/code/'または'./pub/'。
exl-id: fcad8a5d-47d6-4729-93a4-2410d7710d69
feature: Media
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# pub メディアディレクトリで実行されないカスタムサーバーサイドスクリプト

この記事では、 `./pub/media/` クラウドインフラストラクチャー上のAdobe Commerce アプリケーションのディレクトリ。 以下の理由から、これは予想されるセキュリティ制限です。 `./pub/media/` ディレクトリは書き込み可能です。 スクリプトを実行可能にするには、次のような書き込み不可のディレクトリにスクリプトを配置します `./app/code/` または `./pub/`.

## 影響を受けるバージョン

* クラウドインフラストラクチャー上のAdobe Commerce: 2.1.x 以降、スターターおよびプロプランアーキテクチャ、ウィングおよびレガシーアーキテクチャ

## 問題：スクリプトが実行されない

開始時にカスタムサーバーサイドスクリプトを実行できない。

例えば、エンドユーザー（Adobe Commerce買い物客）が `\*.php` スクリプトを含むファイル（例： *domain.com/media/directory/script.php* ）に設定されている場合は、を実行する代わりに、スクリプトがダウンロードされています。

## 原因：スクリプト ファイルの場所が正しくありません

この問題は、スクリプトファイルがに配置されている場合に発生します `./pub/media/` クラウドインフラストラクチャー上のAdobe Commerce アプリケーションのディレクトリ。 これは想定されている動作です。セキュリティ上の制限により、書き込み可能ディレクトリ （`./pub/media/`）が実行されることはありません。

## 解決策：書き込み不可能なディレクトリにスクリプトを配置します

サーバーサイドのスクリプトを、次のような書き込み不可のディレクトリに格納します。 `./app/code/` または `./pub/`  “

## 関連ドキュメント

* [Cloud for Adobe Commerce/プロジェクト構造/書き込み可能ディレクトリ](https://devdocs.magento.com/guides/v2.3/cloud/project/project-start.html#write-dir) 開発者向けドキュメントを参照してください。
