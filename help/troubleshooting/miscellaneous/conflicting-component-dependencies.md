---
title: コンポーネントの依存関係が競合しています
description: この記事では、コンポーネントの依存関係が競合する場合の解決策を示します。 Web Setup Wizard を使用してAdobe Commerceをセットアップまたは更新しようとすると、「We found conflicting component dependencies」* Composer エラーメッセージが表示されます。
exl-id: 782049c4-b6e1-4ead-a00f-80d2aa8475c9
feature: Configuration
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# コンポーネントの依存関係が競合しています

この記事では、コンポーネントの依存関係が競合する場合の解決策を示します。 Web セットアップウィザードを使用してAdobe Commerceをセットアップまたは更新しようとすると、*「競合するコンポーネントの依存関係が見つかりました」* という Composer エラーメッセージが表示されます。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.2.x、2.3.x
* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x
* Magento Open Source2.2.x, 2.3.x


## 問題 {#issue}

次のようなコンポーネントの依存関係の競合エラーメッセージ（実際のパッケージ名とバージョンは異なります）。

```bash
We found conflicting component dependencies.
You are trying to update package(s) magento/module-sample-data to 1.0.0-beta
We have detected conflicts with the following packages:
- magento/sample-data version 0.74.0-beta15. Please try to update it to one of the following package versions: 0.74.0-beta16, 0.74.0-beta14, 0.74.0-beta13, 0.74.0-beta12, 0.74.0-beta11, 0.74.0-beta10, 0.74.0-beta9, 0.74.0-beta8, 0.74.0-beta7
```

## 原因：

このメッセージは、インストールまたは更新するコンポーネントを Composer が特定できない場合に表示されます。

## 解決策

2 つの主なシナリオが原因で、コンポーネントの依存関係が競合する可能性があります。 シナリオをクリックしてトラブルシューティング手順を取得します。

* [Adobe Commerceのアップグレード](#upgrading-magento)
* [サードパーティモジュールとの非互換性：](#incompatibility-third-party-modules)
   * [Adobe Commerce（すべてのデプロイメントタイプ）](#magento-commerce-magento-commerce-cloud)
   * [Magento Open Source](#opensource)

## Adobe Commerceのアップグレード {#upgrading-magento}

クラウドインフラストラクチャー上でAdobe Commerceをアップグレードしている場合は、以下の手順を実行して競合するコンポーネントの依存関係を解決してください。

* アップグレードに使用するキーを確認します。 キーは正しいメールアカウントから生成されていますか？
* 権限を確認し、Magentoのアップグレード要件に一致していることを確認します。 開発者向けドキュメントで、[Magentoのアップグレードの概要/更新およびアップグレードのチェックリスト/ファイルシステムの権限 ](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/prerequisites#verify-file-system-permissions) を確認してください。

## サードパーティモジュールとの非互換性： {#incompatibility-third-party-modules}

コンポーネントの依存関係の競合は、インストールしたものよりも古いCommerce コンポーネントに依存しているサードパーティモジュールが原因で発生することもあります。 次の操作を試してください。

1. 上記の [ 例 ](#issue) では、インストールされたパッケージ magento/sample-data バージョン 0.74.0-beta15 を 1.0.0-beta にアップグレードすることはできません。 ただし、0.74.0-beta15 は 0.74.0-beta16 （またはその他）にアップグレードできます。 `composer.json` を編集して、これらの変更を加えます。 通常、プロジェクトが要求するバージョンは、その JSON ファイル内のオブジェクトの `require` または `require-dev` プロパティで定義されます。 提供されるパッケージバージョンのオプションに応じて、特定のバージョンまたは制約を指定する場合があります。 Composer の使用方法に関する一般的なガイダンスは、アドビのクラウドインフラストラクチャを使用している場合は、開発者向けドキュメントの [Cloud for Adobe Commerce/テクノロジーと要件/Composer](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/overview#files) を参照してください。 Adobe Commerceをオンプレミスで使用している場合は、[Adobe Commerce/インストールガイド/Composer を使用したAdobe Commerceのインストールを参照してください ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/composer)
1. 次に、準備チェックを試します。 開発者向けドキュメントで、[Adobe Commerce アップグレードの概要/Module Manager を実行する/手順 1 の準備チェック ](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/overview) を確認します。
1. 別のコンポーネント依存関係チェックの失敗メッセージで準備チェックが失敗した場合は、[Adobe Commerce](#magento-commerce-magento-commerce-cloud) または [Magento Open Source](#opensource) のどちらを使用しているかに応じて次のリンクをクリックして、詳細なトラブルシューティング手順を取得します。

## Adobe Commerce {#magento-commerce-magento-commerce-cloud}

1. サポートを受けられるよう、拡張機能の開発者にお問い合わせください。 Commerce Marketplaceから拡張機能を購入したページに、連絡先情報が表示されます。 右側のパネルに表示されている **販売者に連絡** ボタンを探します。 すべてのCommerce開発者は、Marketplace で拡張機能を公開する際に、ユーザーおよびインストールガイドを提供する必要があります。 両方の画像はランディングページの右側にあります。
1. 販売者から妥当な時間内に回答がない場合は、カスタマーサポートのコミットメントを思い出させるために、[Marketplace サポートにお問い合わせ ](mailto:commercemarketplacesupport@adobe.com) ください。

## Magento Open Source {#opensource}

Open Sourceの問題を支援する [ メインフォーラム ](https://community.magento.com/) でサポートをリクエストするか、[Adobe Commerce パートナーにお問い合わせください ](https://magento.com/find-a-partner)。
