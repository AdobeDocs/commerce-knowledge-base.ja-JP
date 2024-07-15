---
title: DHL 配送を引き続き提供するには、v10 DHL スキーマにアップグレードしてください
description: この記事では、2022 年 12 月に DHL スキーマ 6.2 が非推奨（廃止予定）になった後も、スキーマ 10.0 にアップグレードするか、AC-3023 パッチを適用することで、マーチャントが DHL 配送を引き続き提供できるソリューションを提供します。
exl-id: eed83713-2d6a-4360-bfa1-bebd4d604f2f
feature: Orders, Shipping/Delivery, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# DHL 配送を引き続き提供するには、DHL スキーマのバージョン 10.0 にアップグレードしてください

この記事では、2022 年 12 月末に DHL スキーマバージョン 6.2 が非推奨（廃止予定）になった後も、マーチャントが DHL 配送を引き続き提供できるようにするソリューションを提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.5 以前のバージョン、すべてのデプロイメント方法。

## 問題

2022 年 8 月に、マーチャントが DHL 配送を引き続き提供できるように、[DHL スキーマバージョン 6.2 のアップグレード ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/adobe-commerce-dhl-upgrade-patch.html) 修正パッチと共に）リリースされました。 DHL では再び新しいスキーマ（バージョン 10.0）を 2022 年 10 月に導入し、以前のバージョン（6.2 スキーマ）は 2022 年 12 月末に非推奨（廃止予定）になります。 Adobe Commerce 2.4.5 以前の DHL 統合では、バージョン 6.2 のみがサポートされています。

## 解決策

2022 年 10 月にリリースされたAdobe Commerce 2.4.5-p1 および 2.4.4-p2 には、新しい DHL スキーマバージョン 10.0 が含まれています。したがって、2.4.5-p1 および 2.4.4-p2 にアップグレードするマーチャントは、DHL 出荷を引き続き提供するために何もする必要はありません。 2022 年 12 月末に DHL スキーマ 6.2 が廃止される前に、すべてのマーチャントが 2.4.5-p1 および 2.4.4-p2 にアップグレードすることをお勧めします。

2.4.5-p1 および 2.4.4-p2 へのアップグレードを希望しないマーチャントは、2022 年 12 月以降も引き続き DHL 配送を提供する場合、修正パッチを適用する必要があります。

## パッチ

パッチ ID は AC-3023 で、[!DNL Quality Patches Tool] バージョン 1.1.21 で使用できます。

デプロイメント方法に応じて、[!DNL Quality Patches Tool] の使用方法とパッチのインストール方法については、次のリンクを参照してください。

* Adobe Commerceのオンプレミス環境およびMagento Open Source:Adobe Experience Leagueの [ 品質パッチ ツール/使用方法 ](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html)。
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

**パッチは、次のAdobe Commerce バージョン（すべてのデプロイメント方法）に適用されます。**

* 2.3.7、2.4.0、2.4.1、2.4.2、2.4.3、2.4.3-p2、2.4.3-p3、2.4.4

## 役に立つリンク

* [[!DNL Quality Patches Tool] > リリースノ ](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/release-notes.html) ト（Adobe Experience League）

* [[!DNL Quality Patches Tool]:Adobe Experience Leagueでパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) 検索します。

## 関連資料

* [ 配送業者として DHL を引き続き提供するためのパッチを ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/adobe-commerce-dhl-upgrade-patch.html) アドビのサポートナレッジベースで適用してください。

* [ 配送業者 > DHL](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/delivery/shipping-carriers/dhl.html) をユーザーガイドに記載します。
* ユーザーガイドの [ 設定リファレンス/販売/配信方法 ](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/delivery-methods.html)。
