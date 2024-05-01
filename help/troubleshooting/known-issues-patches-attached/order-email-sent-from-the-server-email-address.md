---
title: サーバーの E メール アドレスから送信された注文 E メール
description: この記事では、サーバーのメールアドレスから送信される注文メールに関連する、Adobe Commerce on cloud infrastructure 2.2.4 の既知の問題のパッチを提供します。
exl-id: f32e0c09-e19e-4269-bbba-0533d74a7f49
feature: Communications
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# サーバーの E メール アドレスから送信された注文 E メール

この記事では、サーバーのメールアドレスから送信される注文メールに関連する、Adobe Commerce on cloud infrastructure 2.2.4 の既知の問題のパッチを提供します。

## 問題

注文確認メールが Apache サーバーのメールアドレスから送信されます。 その他のメール（パスワードを忘れた場合など）は、設定されたメールアドレスから送信されます。

<u>再現手順</u>:

1. を使用して注文する **注文確認を送信** ボックスがオンになっています。
1. メールを確認します。

<u>期待される結果</u>:

メールは、Adobe Commerceで設定された送信アドレスから送信されました。

<u>実際の結果</u>:

メールは、使用中の Apache サーバーに設定されたメールアドレスから送信されました。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-10993\_EE\_2.2.4\_v1.composer.patch のダウンロード](assets/MDVA-10993_EE_2.2.4_v1.composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.2.4 上のAdobe Commerce

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* クラウドインフラストラクチャー 2.2.5 上のAdobe Commerce
* クラウドインフラストラクチャー 2.2.6 上のAdobe Commerce
* クラウドインフラストラクチャー 2.2.7 上のAdobe Commerce
* クラウドインフラストラクチャー 2.2.8 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.2.4
* Adobe Commerce オンプレミス 2.2.5
* Adobe Commerce オンプレミス 2.2.6
* Adobe Commerce オンプレミス 2.2.7
* Adobe Commerce オンプレミス 2.2.8
* Adobe Commerce オンプレミス 2.3.0

## パッチの適用方法

手順については、を参照してください [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。

## 添付ファイル
