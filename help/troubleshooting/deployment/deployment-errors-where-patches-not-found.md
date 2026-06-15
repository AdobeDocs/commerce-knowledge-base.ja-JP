---
title: デプロイメントまたは手動アプリケーション中に「パッチが見つかりません」エラーが発生する
description: この記事では、「次のパッチが見つかりませんでした：MDVA-XXXXXXX、ACSD-XXXXX」というエラーが表示される問題の解決策を紹介します。 これらのパッチが現在のMagento バージョンで使用可能かどうかを、「status」コマンド*を使用して確認します。
exl-id: 5a2fd35a-892a-48af-a41f-f275297b3e2e
source-git-commit: be0c72a1759ba172666c7c9409c65a1a388e3f11
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# デプロイメントまたは手動アプリケーション中に「パッチが見つかりません」エラーが発生する

この記事では、インスタンスをアップグレードする際にデプロイメントが失敗し、デプロイメントログに次のパッチが見つからないというエラーが表示される場合の問題に対する解決策を提供します。*次のパッチが見つかりませんでした：MDVA-XXXXX, ACSD-XXXXX。 「status」コマンド*&#x200B;を使用して、現在のMagento バージョンに対するこれらのパッチの可用性を確認します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。

## イシュー

Adobe Commerceのアップグレード中にエラーが発生しました：*次のパッチが見つかりませんでした*。

## 原因

以前に適用した古いバージョンのパッチは適用できないか、新しいバージョンでは使用できなくなりました。

この問題は、インストールされた品質パッチ ツール パッケージ （`magento/quality-patches`）が古い場合にも発生する可能性があります。

例：

ケース 1:
* QPT 1.1.71では、2.4.7-p9のパッチが最初に利用可能だった可能性があります
* 新しいQPT リリース（1.1.72など）では、後で2.4.7-p10のサポートが追加される場合があります
* お客様がCommerceを2.4.7-p10にアップグレードしても、古いQPT バージョンがインストールされたままの場合、QPTは2.4.7-p10に互換性のあるパッチバリアントが存在することを認識しない場合があります

ケース 2:
* QPT 1.1.72でパッチが追加された可能性があります
* お客様が古いQPT バージョンをインストールしたままの場合、QPTはパッチが存在することを認識しません

このような場合、パッチの適用は次のようなメッセージで失敗する可能性があります。

```
Next patches weren't found: ACSD-12345.
Check the availability of these patches for the  current Magento version using the "status" command.
```

これは、インストールされているQPT バージョンが、現在のCommerce バージョンを該当するバージョンのパッチにマッピングできないために発生します。

## Solution

この問題は、`.magento.env.yaml`を通じてパッチを適用するデプロイメントに限定されません。 パッチを手動で適用する場合にも、同じ根本的な問題が発生する可能性があります。

```bash
vendor/bin/magento-patches apply <PATCH_ID>
```

例：

```
Next patches weren't found: ACSD-12345
Check the availability of these patches for the  current Magento version using the "status" command.
```

この場合、コマンドを実行している環境にインストールされているAdobe Commerce バージョンでは、パッチは使用できません。

1. QUALITY_PATCHES セクションの下にある`.magento.env.yaml` ファイルを確認します。例：

   ```yaml
   QUALITY_PATCHES:
    * MDVA-XXXXX
    * ACSD-XXXXX
   ```

1. [品質パッチリリースノート &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/release-notes.html)でパッチ IDを調べ、アップグレードする新しいバージョンのAdobe Commerceに各IDを適用できるかどうかを確認します。
1. アップグレードする新しいバージョンのAdobe Commerceにパッチが適用されない場合は、パッチ IDを`.magento.env.yaml` ファイルから削除します。
1. エラーが示すパッチ IDをすべて確認したら、変更をプッシュして再デプロイします。

## 関連トピックス

* Commerce on Cloud Infrastructure ガイドの[&#x200B; パッチの適用](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=en#apply-a-patch-in-a-local-environment)。

