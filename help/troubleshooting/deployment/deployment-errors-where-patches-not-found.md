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

この記事では、インスタンスをアップグレードする際にデプロイメントが失敗し、デプロイメントログに「*次のパッチが見つかりませんでした：MDVA-XXXXX、ACSD-XXXXX」というエラーが表示される場合の問題に対する解決策を説明します。 現在のMagentoバージョンについては、これらのパッチの「status」コマンドの可用性を確認してください*。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[ サポートされているすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。


## 問題

Adobe Commerceのアップグレード中にエラーが発生しています：*次のパッチが見つかりませんでした*。

## 原因：

以前に適用された、古いバージョンのパッチは、新しいバージョンでは適用されないか使用できなくなりました。

## 解決策

1. 「品質PATCH」セクションの `.magento.env.yaml` ファイルを確認します（例：）。

   ```yaml
   QUALITY_PATCHES:
    - MDVA-XXXXX
    - ACSD-XXXXX
   ```

1. [ 品質向上パッチのリリースノート ](/docs/commerce-operations/tools/quality-patches-tool/release-notes.html) でパッチ ID を調べて、アップグレード先のAdobe Commerceの新しいバージョンにそれぞれを適用できるかどうかを確認します。
1. パッチがアップグレード先の新しいバージョンのAdobe Commerceに適用されない場合は、`.magento.env.yaml` ファイルからパッチ ID を削除します。
1. エラーが示すすべてのパッチ ID を確認したら、変更をプッシュして再デプロイします。

## 関連資料

* Commerce on Cloud Infrastructure ガイドの [ パッチの適用 ](/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=en#apply-a-patch-in-a-local-environment)。
