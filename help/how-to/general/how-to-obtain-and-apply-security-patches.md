---
title: '[!UICONTROL security patch] の取得方法と適用方法'
description: この記事では、リリース済みの [!UICONTROL security patch] を取得して適用する方法について説明しますが、説明は使用できません。
exl-id: 55f2be73-2ccc-4750-a7bd-3058fc2d5107
source-git-commit: 43c8308c6539c53f60fb6457047898a2edd46532
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# [!UICONTROL security patch] ールの取得および適用方法

>[!NOTE]
>オンプレミス環境を使用していて、[!DNL CVS] や [!DNL GitHub] などのバージョン管理システムを使用せずにコードを管理している場合は、web ホストがパッチの適用を支援できる可能性があります。 お気軽にお問い合わせください

この記事では、リリース済みの [!UICONTROL security patch] を取得して適用する方法について説明しますが、説明は使用できません。

## 影響を受ける製品とバージョン

Adobe Commerce オンプレミスおよび Cloud – すべてのバージョン


## 原因：

ほとんどの [!UICONTROL Security Patches] は、適用するための独立したパッチやホットフィックスなしでリリースされており、[!UICONTROL Security Patch] のリリースにアップグレードする必要があります。

## 解決策


### ケース I:

* [ リリースノート ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/release-notes/cloud-tools-suite) に孤立したパッチファイル/ホットフィックスが記載されている場合は、[https://account.magento.comのダウンロードセクションからファイルをダウンロードし ](https://account.magento.com/downloads/view/) ください。 共有アクセスユーザーには、まずアカウント所有者/ライセンス所有者からダウンロード権限が付与されている必要があります。

**注意事項：**

古いバージョンのAdobe Commerce（2.4.4）を使用している場合は、自動で拡張サポートを受けることができます。 使用可能な最新のセキュリティパッチを適用するには、お使いのバージョンが次のサポートされていないバージョンのいずれかである必要があります。

2.4.4 - 2.4.4-p11

サポートされていないバージョン（2.3.x、2.4.0～2.4.3）はサポート対象外です。最新のセキュリティ修正を利用するには、まずサポートされているバージョンにアップグレードする必要があります。

拡張サポートを受けていない場合、パッチの共有をサポートに依頼することもできますが、パッチの適用時に発生する可能性のある問題やエラーは解決できません。

### ケース II:

分離パッチは例外的な場合にのみ提供され、セキュリティ修正を実装するための推奨された形式ではありません。

分離されたパッチファイル/ホットフィックスがリリースノートに記載されていない場合：

* **Cloud:**

1. 一部の [!UICONTROL Security Patches] は、Commerceのクラウドパッチの下の最新バージョンの Cloud Tools Suite （ECE ツール）に含まれている（リリースされている）可能性があります。[ リリースノート ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/release-notes/cloud-tools-suite) を確認し、リリースにセキュリティ修正が記載されている場合は、パッケージをそのバージョンにアップグレードします。
1. リリースノートにセキュリティ修正についての記載がない場合は、引き続きお読みください。

* **クラウドまたはオンプレミス：**

* 分離されたパッチファイルまたはホットフィックスが入手できない場合は、[Cloud](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version) 2.4.X のAdobe Commerceのバージョンを、最新のパッチバージョン 2.4.X-pY にアップグレードしてください。
* 分離されたパッチファイルまたはホットフィックスが入手できない場合は、[Adobe Commerce バージョン On-Premise](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade) 2.4.X を最新のパッチバージョン 2.4.X-pY にアップグレードしてください。

## 関連資料

* [2}Cloud Infrastructure ガイドのCommerce Cloud Adobe Commerce ツールスイートのリリースノート ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/release-notes/cloud-tools-suite) を参照してください *。*
* [2}Cloud Infrastructure ガイドのAdobe Commerce Adobe Commerce バージョンのアップグレード ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version) を参照してください **
