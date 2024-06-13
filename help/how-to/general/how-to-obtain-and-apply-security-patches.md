---
title: の取得と適用方法 [!UICONTROL security patch]
description: この記事では、を取得して適用する方法について説明します。 [!UICONTROL security patch] はリリースされましたが、説明は使用できません。
exl-id: 55f2be73-2ccc-4750-a7bd-3058fc2d5107
source-git-commit: b15a1d008b6cc2bdce797768e6ee7029a747e6da
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# の取得と適用方法 [!UICONTROL security patch]

この記事では、を取得して適用する方法について説明します。 [!UICONTROL security patch] はリリースされましたが、説明は使用できません。

## 影響を受ける製品とバージョン

Adobe Commerce オンプレミスおよび Cloud – すべてのバージョン

## 原因：

Most [!UICONTROL Security Patches] は、適用する物理ファイルまたはホットフィックスなしでリリースされます。

## 解決策


### ケース I:

リリースノートに物理的なパッチファイル/ホットフィックスが記載されている場合：

* の「ダウンロード」セクションからファイルをダウンロードします [https://account.magento.com](https://account.magento.com/downloads/view/). （共有アクセス ユーザーには、まずアカウント所有者/ライセンス所有者からダウンロード権限が付与される必要があります）

**注意事項：**

古いバージョンのAdobe Commerceで拡張サポートを購入している場合、セキュリティパッチを適用するには、お使いのバージョンが次のいずれかである必要があります。

* 2.4.2-p2
* 2.4.3-p3

拡張サポートを受けていない場合、パッチの共有をサポートに依頼することもできますが、パッチの適用時に発生する可能性のある問題やエラーは解決できません。

### ケース II:

リリースノートに物理的なパッチファイル/ホットフィックスが記載されていない場合：

* **クラウド：**

1. 一部 [!UICONTROL Security Patches] Commerceのクラウドパッチの下で、最新バージョンの Cloud Tools Suite （ECE ツール）に含まれる/リリースされる可能性があります。 [リリースノート](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/release-notes/cloud-tools-suite)また、リリースでセキュリティ修正が記載されている場合は、パッケージをそのバージョンにアップグレードします。
1. リリースノートにセキュリティ修正についての記載がない場合は、引き続きお読みください。

* **クラウドまたはオンプレミス：**

* 物理的なパッチファイル/ホットフィックスが利用できない場合、 [cloud でのAdobe Commerceのバージョンのアップグレード](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version) 2.4.X から最新のパッチバージョン 2.4.X-pY
* 物理的なパッチファイル/ホットフィックスが利用できない場合、 [オンプレミスでのAdobe Commerce バージョンのアップグレード](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade) 2.4.X から最新のパッチバージョン 2.4.X-pY

## 関連資料

* 参照： [Commerce Cloudツールスイートのリリースノート](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/release-notes/cloud-tools-suite) が含まれる *クラウドインフラストラクチャー上のAdobe Commerce ガイド*.
* 参照： [Adobe Commerceのバージョンのアップグレード](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version) が含まれる *クラウドインフラストラクチャー上のAdobe Commerce ガイド*.
