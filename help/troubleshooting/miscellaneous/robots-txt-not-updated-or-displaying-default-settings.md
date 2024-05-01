---
title: robots.txt が更新されない、またはデフォルト設定が表示されない
description: この記事では、「robots.txt」を正しく設定した場合（例：[Adobe Commerce robots.txt のベストプラクティス ] （https://support.magento.com/hc/en-us/articles/360048754931）に従って、「robots.txt」が更新されない、またはデフォルト設定が表示される場合）の解決策を説明します。
exl-id: 629b1247-9282-49f9-ada3-a804ddbaa0f5
feature: Configuration
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# robots.txt が更新されない、またはデフォルト設定が表示されない

この記事では、を設定した場合の解決策を説明します `robots.txt` 正しく、例：に従う [Adobe Commerce robots.txt のベストプラクティス](https://support.magento.com/hc/en-us/articles/360048754931) しかし、 `robots.txt` が更新されないか、デフォルト設定が表示される。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.x、2.4.x

## 問題

デフォルトを変更できません `robots.txt` の設定値。

<u>再現手順：</u>

1. 管理パネルにアクセスします。
1. コンテンツの追加先 **コンテンツ** > デザイン > **設定** > **のカスタム指示を編集`robots.txt`** テキスト「hello」などのファイルに入力し、変更内容を保存します。
1. にアクセスします `robots.txt` url。

<u>期待される結果：</u>
`robots.txt` には、保存されたテキストがあります。

<u>実際の結果：</u>

`robots.txt` ファイルは変更されません。

## 原因：

検索エンジンによるインデックス作成がオフになっています。

## 解決策

検索エンジンによるインデックス作成を有効にします。 参照： [検索エンジンによるインデックス作成の設定](https://devdocs.magento.com/cloud/trouble/robots-sitemap.html#configure-indexing-by-search-engine) 開発者向けドキュメントを参照してください。

## 関連資料

* [サイトマップと検索エンジンロボットを追加](https://devdocs.magento.com/cloud/trouble/robots-sitemap.html) 開発者向けドキュメントを参照してください。
