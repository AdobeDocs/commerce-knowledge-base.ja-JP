---
title: パッチが見つからないデプロイメントエラー
description: 「この記事では、「次のパッチが見つかりませんでした：MDVA-XXXXX、ACSD-XXXXX」というエラーが表示される問題の解決策を説明します。 最新のMagentoバージョン*については、これらのパッチの「status」コマンドの可用性を確認してください。」
exl-id: 5a2fd35a-892a-48af-a41f-f275297b3e2e
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# パッチが見つからないデプロイメントエラー

この記事では、インスタンスのアップグレード時にデプロイメントが失敗し、デプロイメントログにエラーが表示される場合の問題の解決策を説明します。 *次のパッチは見つかりませんでした：MDVA-XXXXX, ACSD-XXXXX。 現在のMagentoバージョンについては、これらのパッチの「status」コマンドの可用性を確認してください*.

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce [すべてのサポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf).


## 問題

Adobe Commerceのアップグレード中にエラーが発生しています。 *次のパッチが見つかりませんでした*.

## 原因：

以前に適用された、古いバージョンのパッチは、新しいバージョンでは適用されないか使用できなくなりました。

## 解決策

1. を確認 `.magento.env.yaml` 品質PATCHセクションの下のファイル（例：）

   ```yaml
   QUALITY_PATCHES:
    - MDVA-XXXXX
    - ACSD-XXXXX
   ```

1. でパッチ ID を検索する [品質向上パッチのリリースノート](/docs/commerce-operations/tools/quality-patches-tool/release-notes.html) アップグレード先のAdobe Commerceの新しいバージョンにそれぞれのプロファイルが対応しているかどうかを確認するには、
1. パッチがアップグレード先の新しいバージョンのAdobe Commerceに適用されない場合は、からパッチ ID を削除します。 `.magento.env.yaml` ファイル。
1. エラーが示すすべてのパッチ ID を確認したら、変更をプッシュして再デプロイします。

## 関連資料

* [パッチの適用](/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=en#apply-a-patch-in-a-local-environment) （クラウドインフラストラクチャー上のCommerceに関するガイド）を参照してください。
