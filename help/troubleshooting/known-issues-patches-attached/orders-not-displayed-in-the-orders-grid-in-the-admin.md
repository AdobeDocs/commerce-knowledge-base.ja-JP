---
title: 管理の注文グリッドに表示されない注文
description: この記事では、Commerce Admin の注文グリッドに表示されない注文に関連する、Adobe Commerce 2.2.1 の既知の問題に対するパッチを提供します。
exl-id: b8376760-6558-41ed-8c6b-51c5759e831a
feature: Admin Workspace, B2B, Cloud, Paas
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 管理の注文グリッドに表示されない注文

この記事では、Commerce Admin の注文グリッドに表示されない注文に関連する、Adobe Commerce 2.2.1 の既知の問題に対するパッチを提供します。

## 問題

B2B 拡張機能がインストールされたAdobe Commerce 2.2.1 では、登録されたお客様がストアフロントで作成した注文は、Commerce Admin のお客様のアカウントにある注文リストに表示されません。 デバッグログ（`./var/log/debug.log`）、次のエラーがログに記録されます。

`report.CRITICAL: You cannot define a correlation name ‘company_order’ more than once`

<u>前提条件</u>:

ストアカタログにAdobe Commerceのサンプルデータではなく商品が含まれており、B2B 拡張機能がインストールされている。

<u>再現手順</u>:

1. ストアフロントに移動し、カスタマーアカウントを作成します。
1. 商品を買い物かごに追加し、チェックアウトを完了して注文を送信します。
1. 管理者にログインします。
1. に移動します。 **顧客、** 次に、を選択します **すべての顧客**.
1. 新しく作成した顧客に対して、次のボタンをクリックします。 **編集**.
1. クリック **注文件数** 左側のパネル。

<u>期待される結果</u>:

最近送信された注文がグリッドに表示されます。

<u>実際の結果</u>:

注文グリッドが表示されません。 代わりに、空白のページが表示されます。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-7868\_EE\_2.2.1\_v1\_composer.patch のダウンロード](assets/MDVA-7868_EE_2.2.1_v1_composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* Adobe Commerce オンプレミス 2.2.1

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* クラウドインフラストラクチャー上のAdobe Commerce（2.2.0 から 2.2.3 へ）
* Adobe Commerce オンプレミス 2.2.0 および 2.2.2 ～ 2.2.3

## パッチの適用方法

参照： [Adobe Commerceが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで、の手順を確認します。

## 添付ファイル
