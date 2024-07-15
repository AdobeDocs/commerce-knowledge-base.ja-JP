---
title: 依存関係混乱攻撃に対する Composer プラグイン
description: この記事では、依存関係の混乱の攻撃用にリリースされた composer プラグインに関する情報と、エラー回避の推奨事項を説明します。 Composer プラグインは、Adobe Commerce 2.4.3 リリースと共に導入され、Adobe Commerceのマーチャントを Dependency Confusion 攻撃から保護します。
exl-id: 42543043-cf60-4431-80e9-866771c5c87b
feature: Observability
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# 依存関係混乱攻撃に対する Composer プラグイン

この記事では、依存関係の混乱の攻撃用にリリースされた composer プラグインに関する情報と、エラー回避の推奨事項を説明します。 Composer プラグインは、Adobe Commerce 2.4.3 リリースと共に導入され、Adobe Commerceのマーチャントを Dependency Confusion 攻撃から保護します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.3 および今後のバージョン（すべてのデプロイメント方法）

## 問題

Composer のインストールまたはアップデート時に composer プラグインによって `composer.json` で定義された直接または間接の依存関係の少なくとも 1 つを介して、アクティブな依存関係の混乱攻撃が発生し `magento/composer-dependency-version-audit-plugin` 可能性があるケースが検出されます。

<u> 再現手順 </u>:

Composer をインストール/アップデートすると、Dependency Confusion 攻撃の可能性が検出された場合、Composer プラグインはプロセスを停止します。 その場合、Composer のインストール/アップデートは失敗し、次のようなエラーメッセージが表示されます。

*```Higher matching version x.x.x of package/name was found in public repository packagist.org than x.x.x in private.repo. Public package might've been taken over by a malicious entity; please investigate and update package requirement to match the version from the private repository.```*

## 原因：

依存性の混乱攻撃は、PHP の Composer のような依存性マネージャを騙して、プライベートリポジトリからオリジナルのパッケージではなくパブリックなソースから悪意のあるパッケージをダウンロードすることで、サーバ上の任意のコードをリモートで実行することを可能にします。

このような攻撃は、攻撃者が元のパッケージの機能を維持できたとしても、検出されない可能性があります。

パッケージがプライベートリポジトリを通じてのみ利用可能で、公開リポジトリに登録されていない場合、攻撃者はこの脆弱性を不正利用する可能性があります。 次に、攻撃者は、同じ名前のパッケージを公開リポジトリにアップロードし、非公開で使用可能なパッケージよりも高いバージョンを提供します。 次に、依存関係マネージャーは、非公開パッケージと公開パッケージの両方のバージョンを比較し、公開リポジトリーから最も新しいバージョンを選択します。 依存関係マネージャーによってダウンロードされた悪意のあるコードは、アプリケーションのコードと同じ権限で実行されます。

## 解決策

### 商人へのRecommendations

* プラグインが composer のインストール/アップデートを深刻に停止した場合に表示されるエラーメッセージを受け取り、侵害された可能性があるパッケージを認識した場合は、拡張機能の開発者に連絡してください。
* Marketplace または別の信頼できるプライベートリポジトリから、安全なバージョンのパッケージを使用して、Adobe Commerceをインストールできます。
* composer のインストール/アップデートを続行するには、composer.json の必要なパッケージバージョンを Marketplace で見つかった正確なバージョンに変更します。

### 拡張機能開発者からの期待

* 公開リポジトリから入手したプラグインのパッケージが侵害されているかどうかを確実に把握する方法はありません。 このプラグインは、packagist.orgにあるパッケージの公開バージョンが、[repo.magento.com](https://repo.magento.com) などのプライベートリポジトリから入手できるバージョンよりも高い場合に検出します。 拡張機能の開発者は、このような状況を避け、[repo.magento.com](https://repo.magento.com) で入手できるバージョンよりも新しいバージョンを公開しないことを強くお勧めします。
* Adobe Commerceは、Marketplace レビュープロセスによって拡張機能リリースの提供が遅れる可能性があることを理解しています。ただし、マーチャントの安全を維持し、拡張機能の開発者が誤って見逃した可能性のあるミスを見つけやすくするために、このプロセスが存在しています。
