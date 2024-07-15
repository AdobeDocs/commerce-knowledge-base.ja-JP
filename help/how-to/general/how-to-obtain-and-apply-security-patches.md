---
title: '[!UICONTROL security patch] の取得方法と適用方法'
description: この記事では、リリース済みの [!UICONTROL security patch] を取得して適用する方法について説明しますが、説明は使用できません。
exl-id: 55f2be73-2ccc-4750-a7bd-3058fc2d5107
source-git-commit: b15a1d008b6cc2bdce797768e6ee7029a747e6da
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# [!UICONTROL security patch] ールの取得および適用方法

この記事では、リリース済みの [!UICONTROL security patch] を取得して適用する方法について説明しますが、説明は使用できません。

## 影響を受ける製品とバージョン

Adobe Commerce オンプレミスおよび Cloud – すべてのバージョン

## 原因：

ほとんどの [!UICONTROL Security Patches] は、適用する物理ファイルまたはホットフィックスなしでリリースされます。

## 解決策


### ケース I:

リリースノートに物理的なパッチファイル/ホットフィックスが記載されている場合：

* [https://account.magento.com](https://account.magento.com/downloads/view/) のダウンロードセクションからファイルをダウンロードします。 （共有アクセス ユーザーには、まずアカウント所有者/ライセンス所有者からダウンロード権限が付与される必要があります）

**注意事項：**

古いバージョンのAdobe Commerceで拡張サポートを購入している場合、セキュリティパッチを適用するには、お使いのバージョンが次のいずれかである必要があります。

* 2.4.2-p2
* 2.4.3-p3

拡張サポートを受けていない場合、パッチの共有をサポートに依頼することもできますが、パッチの適用時に発生する可能性のある問題やエラーは解決できません。

### ケース II:

リリースノートに物理的なパッチファイル/ホットフィックスが記載されていない場合：

* **Cloud:**

1. 一部の [!UICONTROL Security Patches] は、Commerceのクラウドパッチの下の最新バージョンの Cloud Tools Suite （ECE ツール）に含まれている（リリースされている）可能性があります。[ リリースノート ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/release-notes/cloud-tools-suite) を確認し、リリースにセキュリティ修正が記載されている場合は、パッケージをそのバージョンにアップグレードします。
1. リリースノートにセキュリティ修正についての記載がない場合は、引き続きお読みください。

* **クラウドまたはオンプレミス：**

* 物理的なパッチファイルまたはホットフィックスが入手できない場合は、[Cloud](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version) 2.4.X のAdobe Commerceのバージョンを、最新のパッチバージョン 2.4.X-pY にアップグレードしてください。
* 物理的なパッチファイルまたはホットフィックスが入手できない場合は、[Adobe Commerce バージョン On-Premise](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade) 2.4.X を最新のパッチバージョン 2.4.X-pY にアップグレードしてください。

## 関連資料

* [2}Cloud Infrastructure ガイドのAdobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/release-notes/cloud-tools-suite)Commerce Cloudツールスイートのリリースノート *を参照してください。*
* [2}Cloud Infrastructure ガイドのAdobe Commerce Adobe Commerce バージョンのアップグレード ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version) を参照してください **
