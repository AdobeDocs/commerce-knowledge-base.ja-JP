---
title: Adobe Commerce 2.4.1 および 2.3.6 「アカウントを作成」ボタンが無効になっているホットフィックス
description: この記事では、フォームの任意のフィールドに誤った値を入力した後に新しいアカウントの作成に苦労した場合の問題に対するホットフィックスを提供します。 例えば、誤った形式でメールアドレスを入力した場合、名フィールドまたは姓フィールドを空のままにした場合、パスワード要件を満たす値を入力しなかった場合などです。 永続的な修正は、第 1 四半期のリリース（2.4.2、2.4.1-p1、および 2.3.6-p1）に含まれます。
exl-id: e6e65ede-8156-4e2b-b369-b18395bb3dbf
feature: Customer Service
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Adobe Commerce 2.4.1 および 2.3.6 「アカウントを作成」ボタンが無効になっているホットフィックス

この記事では、フォームの任意のフィールドに誤った値を入力した後に新しいアカウントの作成に苦労した場合の問題に対するホットフィックスを提供します。 例えば、誤った形式でメールアドレスを入力した場合、名フィールドまたは姓フィールドを空のままにした場合、パスワード要件を満たす値を入力しなかった場合などです。 永続的な修正は、第 1 四半期のリリース（2.4.2、2.4.1-p1、および 2.3.6-p1）に含まれます。

## 問題

この **アカウントの作成** のボタン **新しいアカウントを作成** 買い物客が無効なデータを入力した場合、ページは無効のままになります。 これにより、買い物客がエラーを起こした後にアカウントを再作成するのを防ぎます。

<u>再現手順</u>:

1. に移動 **新しい顧客アカウントを作成**.
1. フォームフィールドに入力します。 が含まれる **パスワード** フィールド、パスワード要件を満たさない入力値。 例：
   * のパスワード **パスワード** および **パスワードの確認** フィールドが一致しません。
   * のパスワード **パスワード** および **パスワードの確認** フィールドの長さが十分ではありません。
1. 「」をクリックします **アカウントの作成** ボタン。

<u>期待される結果</u>:

* **アカウントの作成** ボタンはアクティブ/有効のままにする必要があります。
* ユーザーは新しいアカウントを作成できます。

<u>実際の結果</u>:

* **アカウントの作成** 有効または正しいデータを含むすべての必須フィールドに入力した後でも、ボタンは無効のままです。
* お客様は新しいアカウントを作成できません。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。 [MC-38509-composer.patch のダウンロード](assets/MC-38509-composer.patch.zip)

## 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.3.6 および 2.4.1 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.3.6 および 2.4.1。

このパッチは、他のAdobe Commerce バージョンおよびエディションとは互換性がありません。

## パッチの適用方法

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 説明を参照してください。

## 関連資料

* [GitHub Adobe Commerce /無効なアカウント作成フォームを送信すると、送信ボタンが無効のままになる](https://github.com/magento/magento2/issues/30513)
* [Adobe Commerce ユーザーガイド /はじめに/ アカウントの作成](https://docs.magento.com/user-guide/magento/magento-account-create.html)