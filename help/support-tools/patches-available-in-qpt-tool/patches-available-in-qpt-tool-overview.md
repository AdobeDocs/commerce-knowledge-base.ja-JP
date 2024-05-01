---
title: QPT ツールで使用可能なパッチの概要
description: この記事では、の概要を説明します [!DNL Quality Patches Tool] （QPT）とその使用方法を説明するリソースへのリンク。
exl-id: ac1c6088-44fe-452c-a39b-3c35697e1cc3
feature: Support, Tools and External Services
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# QPT ツールで使用可能なパッチの概要

この記事では、の概要を説明します [!DNL Quality Patches Tool] （QPT）とその使用方法を説明するリソースへのリンク。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス、すべて [サポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)
* クラウドインフラストラクチャー上のAdobe Commerce、すべて [サポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 品質向上パッチツールとは

この [[!DNL Quality Patches Tool]](https://github.com/magento/quality-patches) （QPT）は、AdobeやMagento Open Sourceコミュニティが開発した個別のクオリティパッチを適用できるツールです。

次の操作が可能です。

* パッケージに含まれる品質向上パッチの適用
* 以前に適用したパッチを元に戻す
* インストール済みバージョンのAdobe Commerceで使用可能なクオリティパッチに関する一般情報を表示します。

使用可能なパッチを表示するために取得できるステータステーブルの例を次に示します。

![Magento_パッチ_リスト](assets/status_table.png)

このツールの目的は、Adobe Commerceで発生する可能性のある問題のパッチをセルフサービスで提供できるようにしたり、Adobe Commerce サポートから提案されたパッチを簡単に適用できるようにすることです。

>[!NOTE]
>
>QPT は品質向上パッチ専用です。 セキュリティパッチは、で入手できます。 [Adobe CommerceおよびMagento Open Sourceのリリースノート](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/overview.html).

## で使用可能なパッチ [!DNL Quality Patches Tool]

Adobe Commerce サポートナレッジベースのこのセクションでは、QPT パッチによって解決された問題の詳細な説明を、QPT リリースバージョン別にグループ化して示します。
また、使用可能な QPT パッチのリストを確認し、上の動的に生成されたテーブルを使用して、コンポーネントでフィルタリングすることもできます。 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) サポートナレッジベースで。

## をインストールして使用する方法 [!DNL Quality Patches Tool]

Adobe Commerce オンプレミスの場合と、クラウドインフラストラクチャ上のAdobe Commerceの場合は、インストールコマンドと使用コマンドが異なります。クラウドの場合は、QPT パッケージが ece-tools パッケージに含まれています。

### Adobe Commerce オンプレミスで QPT をインストールして使用する方法

を参照してください。 [Commerce/ ツール /使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) パッチを適用して元に戻すための QPT のインストールおよび使用方法の詳細については、開発者向けドキュメントを参照してください。

### クラウドインフラストラクチャーにAdobe Commerce用 QPT をインストールして使用する方法

を参照してください。 [Commerce on Cloud Infrastructure ガイド > パッチの適用](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) クラウドインフラストラクチャー上で QPT をインストールして使用し、Adobe Commerceにパッチを適用して元に戻す方法について詳しくは、開発者向けドキュメントを参照してください。

## 関連資料

* [[!DNL Quality Patches Tool] リリースノート](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/release-notes.html) 開発者向けドキュメントを参照してください。
