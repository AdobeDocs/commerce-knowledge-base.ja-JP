---
title: Google Analyticsがコンバージョンデータをトラッキングしていない
description: この記事では、コンバージョンデータをトラッキングしないGoogle Analyticsに関連する、Adobe Commerce 2.2.4 の既知の問題に対するパッチを提供します。
exl-id: b9012fd1-4f90-41e9-9559-0343ee052ec6
feature: Configuration, Observability
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Google Analyticsがコンバージョンデータをトラッキングしていない

この記事では、コンバージョンデータをトラッキングしないGoogle Analyticsに関連する、Adobe Commerce 2.2.4 の既知の問題に対するパッチを提供します。

>[!NOTE]
>
>この問題は、Adobe Commerce 2.2.6 で修正されました。

## 問題

Google Analytics コンポーネントコードのエラーにより、コンバージョンデータがGoogle Analyticsで追跡されませんでした。

<u>再現手順</u>:

1. の下のCommerce Admin でGoogle Analytics機能を有効にして設定します。 **ストア** > **設定** > **設定** > **売上** > **GOOGLE API** > **Google Analytics**.
1. クリック **設定を保存**.
1. 店頭で注文します。
1. に移動 **Google Analyticsダッシュボード** > **コンバージョン** > **概要**.
1. 日付範囲を現在の日付に設定します。

<u>期待される結果</u>:

この順序は、コンバージョンデータに表示されます。

<u>実際の結果</u>:

順序は、コンバージョンデータには表示されません。

## 解決策

このパッチにより、Google Analyticsコンポーネントコードのエラーが修正されます。 パッチ適用後は、Google Analyticsがコンバージョンデータを追跡します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-11263\_EE\_2.2.4\_v1.composer.patch のダウンロード](assets/MDVA-11263_EE_2.2.4_v1.composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* Adobe Commerce オンプレミス 2.2.4

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* Adobe Commerce オンプレミス 2.2.5
* クラウドインフラストラクチャー上のAdobe Commerce 2.2.4、2.2.5

## パッチの適用方法

参照： [Adobe Commerceが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 説明を参照してください。

## 添付ファイル
