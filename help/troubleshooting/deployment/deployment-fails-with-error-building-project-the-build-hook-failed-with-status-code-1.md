---
title: 「プロジェクトの構築エラー：ビルドフックがステータスコード 1 で失敗しました」でデプロイメントが失敗する」
description: 「この記事では、デプロイメントプロセスのビルドフェーズが失敗するクラウドインフラストラクチャ上のAdobe Commerceの問題の原因と解決策について説明します。エラーメッセージは次のように要約されます。*「エラー構築プロジェクト：ビルドフックがステータスコード 1 で失敗しました」*。
exl-id: add1cdac-dbcb-4c55-8bc2-c1f27e24aadb
feature: Build, Deploy
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 0%

---

# 「プロジェクトの構築エラー：ビルドフックがステータスコード 1 で失敗しました」でデプロイメントが失敗します

この記事では、デプロイメントプロセスのビルド段階が失敗し、エラーメッセージが次のように要約されるクラウドインフラストラクチャ上のAdobe Commerceの問題の原因と解決策について説明します。 *「プロジェクトの構築エラー：ビルドフックがステータスコード 1 で失敗しました」*.

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

<u>再現手順</u>:

手動で、または環境の結合、プッシュまたはトリガーを実行して、デプロイメントを同期します。

<u>期待される結果</u>:

デプロイメントが正常に完了しました。

<u>実際の結果</u>:

1. 構築フェーズが失敗し、デプロイメントプロセス全体が停止します。
1. デプロイメントエラーログで、エラーメッセージが次の文字列で終わる。 *「プロジェクトの構築エラー：ビルドフックがステータスコード 1 で失敗しました。 ビルドが中止されました」というエラーメッセージが表示されます。*

## 原因：

環境の構築が失敗する理由は複数あります。 通常、デプロイメントログには長いエラーメッセージが表示されます。最初の部分が理由についてより具体的であり、結論は次のようになります *「プロジェクトの構築エラー：ビルドフックがステータスコード 1 で失敗しました。 ビルドが中止されました」というエラーメッセージが表示されます。*

最初の問題固有の部分を詳しく見ると、問題を特定するのに役立ちます。 以下に、最も一般的な例を示します。次のセクションでは、それらのソリューションについて説明します。

* 使用可能な記憶域がありません。
* ECE ツールの設定が正しくありません。
* 適用しようとしているパッチは、お使いのAdobe Commerceのバージョンと互換性がないか、適用されている他のパッチまたはカスタマイズと競合しています。
* カスタムモジュールコードの問題により、が正常にビルドされません。

## 解決策

* 十分なストレージがあることを確認します。 使用可能な領域を確認する方法については、を参照してください [CLI を使用したクラウド環境上のディスク容量の確認](/help/how-to/general/check-disk-space-on-cloud-environment-using-cli.md) 記事。 ログディレクトリのクリーニングやディスク容量の増加を検討できます。
* ECE ツールが正しく設定されていることを確認します。
* 問題の原因がパッチであるかどうかを確認します。 競合または連絡先を解決する [Adobe Commerce サポート](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket). 詳しくは、以下を参照してください。
* 問題の原因がカスタム拡張機能であるかどうかを確認します。 競合を解決するか、拡張機能の開発者にソリューションを問い合わせてください。

以下の段落で、詳しい説明を紹介します。

### ログをクリーンアップしたり、領域を増やしたりします

クリーンアップの対象となるディレクトリ：

* `var/log`
* `var/report`
* `var/debug/`
* `var`

Adobe Commerce on cloud infrastructure スタータープランアーキテクチャを使用している場合に、ディスク容量を増やす方法について詳しくは、を参照してください。 [クラウド上の統合環境のディスク容量を増やす](/help/how-to/general/increase-disk-space-for-integration-environment-on-cloud.md). 同じ手順を使用して、クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャの統合環境の容量を増やすことができます。 実稼動/ステージング環境の場合は、にチケットを提出する必要があります。 [Adobe Commerce サポート](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)、およびリクエストして、ディスク容量を増やしました。 しかし、それはプラットフォームによって監視されます。 ただし、通常は、Adobe Commerceがこれらのパラメーターをモニタリングし、アラートを送信したり、契約に従ってアクションを実行したりするので、Pro アーキテクチャのステージング/実稼動で対処する必要はありません。

### ECE ツールが正しく設定されていることを確認します。

1. ビルドフックがで正しく定義されていることを確認します。 `magento.app.yaml` ファイル。 Adobe Commerce 2.2.X を使用している場合、ビルドフックは次のように定義する必要があります。

   ```yaml
   # We run build hooks before your application has been packaged.
   build: |
       php ./vendor/bin/ece-tools build
   # We run deploy hook after your application has been deployed and started.
   deploy: |
       php ./vendor/bin/ece-tools deploy
   ```

   の使用 [ece-tools へのアップグレード](https://devdocs.magento.com/guides/v2.3/cloud/project/ece-tools-upgrade-project.html) 参照用の記事。

1. ECE ツールパッケージがに存在することを確認します。 `composer.lock` 次のコマンドを実行して、ファイルを指定します。    <pre><code class="language-bash">grep &#39;<code class="language-yaml">「名前」:「magento/ece-tools」</code>&#39; composer.lock</code></pre>    これらを指定した場合、応答は次の例のようになります。    ```bash    "name": "magento/ece-tools",    "version": "2002.0.20",    ```

を参照してください。 [ece-tools へのアップグレード](https://devdocs.magento.com/guides/v2.3/cloud/project/ece-tools-upgrade-project.html) 参照用の記事。

### パッチが原因で問題が発生しているか。

環境が正常に構築されない原因となっている適用されたパッチがある場合は、デプロイログに次のような内容が表示されます。

```bash
%patch_name%.composer.patch
[2019-02-19 18:12:59] CRITICAL:
....
[2019-02-19 18:12:59] CRITICAL: Command git apply --check --reverse /app/m2-hotfixes/%patch_name%.composer.patch returned code 1
...
W:
W: Command git apply --check --reverse /app/m2-hotfixes/%patch_name%.composer.patch returned code 1
W:
W:
W: build
...
E: Error building project: The build hook failed with status code 1. Aborted build.
```

これらのエラーメッセージは、適用しようとしているパッチが別のAdobe Commerce バージョン用に作成されたか、カスタマイズまたは以前に適用されたパッチと競合していることを意味します。 競合または連絡先を解決してみます [Adobe Commerce サポート](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

### 拡張機能が問題の原因ですか？

カスタム拡張機能のために環境を正常にビルドできない場合は、デプロイメントログにカスタムモジュール名と、このモジュールが原因で発生する特定の競合が表示されます。 競合を解決するか、拡張機能の開発者にソリューションを問い合わせてください。

### 変更が適用されていることを確認します

変更をコミットし、プッシュします。 これにより、デプロイメントが自動的にトリガーされます。
