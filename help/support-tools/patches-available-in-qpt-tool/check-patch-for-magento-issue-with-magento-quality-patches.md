---
title: Quality Patches Tool を使用して、Adobe Commerceの問題のパッチを確認します。
description: この記事では、品質向上パッチツール（QPT）の概要と、その使用方法を説明するリソースへのリンクを示します。
exl-id: 43393708-3939-449f-a764-b2ac6326165f
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Quality Patches Tool を使用して、Adobe Commerceの問題のパッチを確認します。

この記事では、品質向上パッチツール（QPT）の概要と、その使用方法を説明するリソースへのリンクを示します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス、すべて [ サポート対象バージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)
* クラウドインフラストラクチャー上のAdobe Commerce、すべて [ サポート対象バージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 品質向上パッチツールとは

[Quality Patches Tool](https://github.com/magento/quality-patches) （QPT）は、AdobeおよびMagento Open Sourceコミュニティが開発した個別のパッチです。

次の操作が可能です。

* パッケージに含まれる品質向上パッチの適用
* 以前に適用したパッチを元に戻す
* インストール済みバージョンのAdobe Commerceで使用可能なクオリティパッチに関する一般情報を表示します。

使用可能なパッチを表示するために取得できるステータステーブルの例を次に示します。

![Magento_パッチ_リスト ](assets/status_table.png)

このツールの目的は、Adobe Commerceで発生する可能性のある問題のパッチをセルフサービスで提供できるようにしたり、Adobe Commerce サポートから提案されたパッチを簡単に適用できるようにすることです。

>[!NOTE]
>
>QPT は品質向上パッチ専用です。 セキュリティ パッチは、[Magento セキュリティ センター ](https://magento.com/security/patches) で入手できます。

## 品質向上パッチツールで使用可能なパッチ

使用可能なパッチのリストについては、開発者向けドキュメントの [Quality Patches Tool](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。

## 品質向上パッチツールのインストール方法と使用方法

Adobe Commerce オンプレミスの場合と、クラウドインフラストラクチャ上のAdobe Commerceの場合は、インストールコマンドと使用コマンドが異なります。クラウドの場合は、QPT パッケージが ece-tools パッケージに含まれています。

### Adobe Commerce オンプレミスで QPT をインストールして使用する方法

パッチの適用と元に戻すための QPT のインストールおよび使用方法の詳細については、開発者向けドキュメントの [ ソフトウェア更新ガイド/パッチ適用 ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) を参照してください。

### クラウドインフラストラクチャーにAdobe Commerce用 QPT をインストールして使用する方法

クラウドインフラストラクチャで QPT をインストールして使用し、Adobe Commerceにパッチを適用したり元に戻したりする方法について詳しくは、開発者向けドキュメントの [Cloud for Adobe Commerce/パッチを適用 ](https://devdocs.magento.com/cloud/project/project-patch.html) を参照してください。

## 関連資料

* 開発者向けドキュメントの [ 品質向上パッチツールのリリースノート ](https://devdocs.magento.com/quality-patches/release-notes.html)
* [Adobeが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) をサポート サポート サポート サポート サポート サポート サポート サポート サポート サポート サポート サポート サポート サポート サポート サポート サポート サポート サポート情報に含めます。
