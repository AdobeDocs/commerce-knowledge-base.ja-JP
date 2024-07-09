---
title: コンポーネントの依存関係が競合しています
description: この記事では、コンポーネントの依存関係が競合する場合の解決策を示します。 Web Setup Wizard を使用してAdobe Commerceをセットアップまたは更新しようとすると、「We found conflicting component dependencies」* Composer エラーメッセージが表示されます。
exl-id: 782049c4-b6e1-4ead-a00f-80d2aa8475c9
feature: Configuration
role: Developer
source-git-commit: 8f0f7412e75e07a22e66236b88c095c698dbf23e
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# コンポーネントの依存関係が競合しています

この記事では、コンポーネントの依存関係が競合する場合の解決策を示します。 Web 設定ウィザードを使用してAdobe Commerceを設定または更新しようとすると、 *「競合するコンポーネントの依存関係が見つかりました」* Composer エラーメッセージ。

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
* 権限を確認し、Magentoのアップグレード要件に一致していることを確認します。 レビュー [Magentoのアップグレードの概要/更新とアップグレードのチェックリスト/ファイルシステムの権限](https://devdocs.magento.com/guides/v2.3/comp-mgr/prereq/prereq_compman-checklist.html#perms) 開発者向けドキュメントを参照してください。

## サードパーティモジュールとの非互換性： {#incompatibility-third-party-modules}

コンポーネントの依存関係の競合は、インストールしたものよりも古いCommerce コンポーネントに依存しているサードパーティモジュールが原因で発生することもあります。 次の操作を試してください。

1. 前項 [例](#issue)の場合、インストールされているパッケージ magento/sample-data バージョン 0.74.0-beta15 を 1.0.0-beta にアップグレードすることはできません。 ただし、0.74.0-beta15 は 0.74.0-beta16 （またはその他）にアップグレードできます。 編集 `composer.json` これらの変更を行います。 通常、プロジェクトがリクエストするバージョンは、 `require` または `require-dev` その JSON ファイル内のオブジェクトのプロパティ。 提供されるパッケージバージョンのオプションに応じて、特定のバージョンまたは制約を指定する場合があります。 Composer の使用方法に関する一般的なガイダンスについては、クラウドインフラストラクチャを使用している場合は、次を参照してください。 [Cloud for Adobe Commerce/技術と要件/Composer](https://devdocs.magento.com/cloud/reference/cloud-composer.html#files) 開発者向けドキュメントを参照してください。 Adobe Commerceをオンプレミスで使用している場合は、を参照してください。 [Adobe Commerce/インストールガイド/Composer を使用したAdobe Commerceのインストール](https://devdocs.magento.com/guides/v2.4/install-gde/composer.html) .
1. 次に、準備チェックを試します。 レビュー [Adobe Commerceのアップグレードの概要/Module Manager の実行/手順 1 の準備状況チェック](https://devdocs.magento.com/guides/v2.3/comp-mgr/module-man/compman-readiness.html) 開発者向けドキュメントを参照してください。
1. 別のコンポーネント依存関係チェック失敗メッセージで準備チェックが失敗した場合は、を使用しているかどうかに応じて、次のリンクをクリックします [Adobe Commerce](#magento-commerce-magento-commerce-cloud) または [Magento Open Source](#opensource) 詳細なトラブルシューティング手順については、を参照してください。

## Adobe Commerce {#magento-commerce-magento-commerce-cloud}

1. サポートを受けられるよう、拡張機能の開発者にお問い合わせください。 Commerce Marketplaceから拡張機能を購入したページに、連絡先情報が表示されます。 を探します。 **販売者に連絡** 右パネルに表示されるボタン。 すべてのCommerce開発者は、Marketplace で拡張機能を公開する際に、ユーザーおよびインストールガイドを提供する必要があります。 両方の画像はランディングページの右側にあります。
1. 売主から相当の期間に回答がない場合は、 [marketplace サポートに連絡](mailto:commercemarketplacesupport@adobe.com) それにより、お客様のカスタマーサポートに対するコミットメントを思い出してもらうことができます。

## Magento Open Source {#opensource}

で支援を依頼する [メインフォーラム](https://community.magento.com/) または [Adobe Commerce パートナーに連絡](https://magento.com/find-a-partner) これは、オープンなSourceの問題に役立ちます。
