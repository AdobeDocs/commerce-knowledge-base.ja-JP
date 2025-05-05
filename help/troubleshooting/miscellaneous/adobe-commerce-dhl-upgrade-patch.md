---
title: 配送業者として DHL を引き続き提供するためのパッチを適用する
description: この記事では、2022 年 7 月末から 9 月に DHL スキーマ 6.0 が非推奨（廃止予定）になった後も、Adobe Commerce 2.4.4 以前を使用しているマーチャントが DHL 配送を引き続き提供できるパッチを提供します。
exl-id: 4350e83a-495b-41b4-a526-dae5923e9d41
feature: Orders, Shipping/Delivery, Upgrade
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 配送業者として DHL を引き続き提供するためのパッチを適用する


## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.4 以前、すべてのデプロイメント方法。

## 問題

DHL は 6.2 スキーマバージョンを導入しており、2022 年 7 月末から 9 月末までにバージョン 6.0 を廃止します。 Adobe Commerce 2.4.4 以前の DHL 統合では、バージョン 6.0 のみがサポートされています。

## 解決策

2022 年 8 月にリリースされる予定のAdobe Commerce 2.4.5 には、バージョン 6.2 スキーマを使用して DHL とのアップグレードされた統合が含まれます。 新しいバージョンがリリースされる（またはアップグレードしない場合）まで、バージョン 6.2 の DHL スキーマのサポートを実装した AC-3022 パッチを適用して、廃止後もストアで DHL の出荷を継続することをお勧めします。

## パッチ

パッチ ID は、Quality Patches Tool バージョン 1.1.16 で使用可能な AC-3022 です。
QPT の使用方法とパッチのインストール方法については、開発者向けドキュメントの [Quality Patches Tool （QPT） > Usage](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage) の記事を参照してください。

このパッチは、次のAdobe Commerce バージョンに適用されます。

* 2.4.0 ～ 2.4.4-p1
* 2.3.7

## 関連資料

* [ 配送業者 > DHL](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/delivery/shipping-carriers/dhl) ユーザーガイド
* ユーザーガイドの [ 配信方法 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/sales/delivery-methods)
