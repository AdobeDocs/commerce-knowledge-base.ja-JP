---
title: 「管理者でテーマ設定を保存する際に「領域は既に設定されています」エラーが発生する」
description: この記事では、Adobe Commerce管理者でデフォルトのストアビューのテーマを設定しようとすると発生する「Area is already set」（領域は既に設定されています）というエラーメッセージに関する、Commerce on cloud infrastructure 2.2.4 の既知の問題のパッチを提供します。
exl-id: c4e34a73-b774-4447-ba8e-aaf208ad54c5
feature: Admin Workspace, Configuration, Themes
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 管理でテーマ設定を保存する際に「領域は既に設定されています」エラーが発生する

この記事では、の取得に関連するAdobe Commerce on cloud infrastructure 2.2.4 の既知の問題に対するパッチを提供します *「エリアは既に設定されています」* Commerce管理でデフォルトのストア表示のテーマを設定しようとするとエラーメッセージが表示されます。

## 問題

「」が表示されます *この構成の保存中にエラーが発生しました：エリアは既に設定されています* デフォルトのストア表示のテーマを設定しようとするとエラーメッセージが表示されます。

<u>再現手順</u>:

1. Commerce Admin にログインします。
1. に移動します。 **コンテンツ** > **デザイン** > **設定**.
1. 設定範囲をに設定します。 *デフォルトのストア表示*.
1. でのテーマの変更 **適用されたテーマ** ドロップダウン。 例：から *Luma* 対象： *空白。*
1. クリック **設定を保存**.

<u>期待される結果</u>：選択したテーマが、デフォルトのストア表示に適用されます。

<u>実際の結果</u> ：テーマが適用されない、 *「この設定の保存中に問題が発生しました：領域は既に設定されています」* エラーメッセージが表示されます。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、次のリンクをクリックするか、記事の最後まで下にスクロールして、添付ファイルをクリックします。

[MDVA-11106\_EE\_2.2.4\_v1.composer.patch のダウンロード](assets/MDVA-11106_EE_2.2.4_v1.composer.patch.zip)

## 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.2.4 上のAdobe Commerce

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* クラウドインフラストラクチャー 2.0.X 上のAdobe Commerce
* クラウドインフラストラクチャー 2.1.X 上のAdobe Commerce
* クラウドインフラストラクチャー上のAdobe Commerce 2.2.0 - 2.2.5
* Adobe Commerce オンプレミス 2.0.X
* Adobe Commerce オンプレミス 2.1.X
* Adobe Commerce オンプレミス 2.2.0 - 2.2.5

## パッチの適用方法

手順については、を参照してください [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。

## 添付ファイル
