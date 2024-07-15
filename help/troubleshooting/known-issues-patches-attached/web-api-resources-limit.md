---
title: Web API が、配列に 20 個を超える項目を含むリクエストを処理できない
description: ここでは、Adobe Commerce 2.4.3 の配列に 20 個を超える項目が含まれているメッセージを Web API で処理できない問題の解決策を説明します。
exl-id: 7e6b3fe8-3133-4773-afa7-fbfdd98ecde9
feature: REST
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Web API が、配列に 20 個を超える項目を含むリクエストを処理できない

ここでは、Adobe Commerce 2.4.3 の配列に 20 個を超える項目が含まれているメッセージを Web API で処理できない問題の解決策を説明します。

## 影響を受ける製品とバージョン：

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 および 2.3.7-p1
* Magento Open Source 2.4.3 および 2.3.7-p1

## 問題

Web API は、配列に 20 個を超える項目を含むメッセージ（例：Stock 更新）を処理できません。

## 原因：

Adobe Commerce 2.4.3 では、サービス拒否（DoS）攻撃を防ぐために、Magento API に組み込みのレート制限が追加されました。

デフォルトでは、次の組み込みの API レート制限を使用できます。

* エンティティのリストを表す入力を含む REST リクエストは、デフォルトの最大 20 エンティティに制限されます
* ページ分割された結果を許可する REST およびGraphQL クエリは、1 ページにつきデフォルトの最大 300 アイテムに制限される

## 解決策

REST API リクエストの入力制限を無効にするには、（バージョンに応じて）次のいずれかのパッチを適用します。

* [MC-43048__set_rate_limits__2.3.7-p1.patch.zip](assets/MC-43048__set_rate_limits__2.3.7-p1.patch.zip)
* [MC-43048__set_rate_limits__2.4.3.patch.zip](assets/MC-43048__set_rate_limits__2.4.3.patch.zip)

### 互換性のあるAdobe Commerce バージョン

パッチは次の場合に作成されました。

* クラウドインフラストラクチャー上のAdobe Commerce 2.4.3 および 2.3.7-p1
* Adobe Commerce オンプレミス 2.4.3 および 2.3.7-p1

パッチは他のAdobe Commerce バージョンとは互換性がありません。

### パッチの適用方法

ダウンロードした `.zip` ファイルを解凍し、[Adobeが提供する Composer パッチを適用する方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) に従ってパッチを適用します。

>[!WARNING]
>
>ストアで DoS 攻撃が発生していると思われる場合、Adobeでは、デフォルトの入力制限を低い値に下げて、リクエストできるリソースの数に制限を設けることをお勧めします。  [ クラスコンストラクター引数を使用すると、プログラムによってデフォルトの制限をカスタマイズでき ](https://devdocs.magento.com/guides/v2.4/extension-dev-guide/build/di-xml-file.html) す。
>開発者向けドキュメント [API セキュリティ/レート制限/最大パラメーター入力 ](https://devdocs.magento.com/guides/v2.4/get-started/api-security.html#rate-limiting) に記載されています。

## 関連資料

開発者向けドキュメントの [API セキュリティ/レート制限 ](https://devdocs.magento.com/guides/v2.4/get-started/api-security.html#rate-limiting)。
