---
title: 新しい注文がアーカイブに送信される
description: この記事では、新しく作成された注文がCommerce Admin の注文グリッドではなくアーカイブに表示されることに関連する、既知のAdobe Commerce 2.2.0 の問題のパッチを提供します。
exl-id: 37b70d28-0569-44f2-b677-29b2bde0bc5c
feature: Storage, Data Import/Export
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 新しい注文がアーカイブに送信される

この記事では、新しく作成された注文がCommerce Admin の注文グリッドではなくアーカイブに表示されることに関連する、既知のAdobe Commerce 2.2.0 の問題のパッチを提供します。

>[!NOTE]
>
>この問題は、2.2.3 以降で修正されました。

## 問題

顧客が注文すると、通常の注文グリッドではなく、アーカイブ済み注文グリッドに表示されます。

<u>再現手順</u>:

1. 商品をストアフロントのカートに追加し、チェックアウトを進め、注文します。
1. Commerce Admin で、に移動します。 **売上** > **運用** > **順序**. グリッドに表示される順序を確認します。
1. に移動します。 **売上** > **アーカイブ** > **注文件数**. グリッドに新しい順序が表示されます。

<u>期待される結果</u>:

注文は注文グリッドにのみ表示されます。

<u>実際の結果</u>:

注文は [ 注文 ] グリッドと [ 注文アーカイブ ] グリッドに表示されます。

## 解決策

パッチを適用すると、注文が期待どおりに注文グリッドに表示されます。 ただし、パッチを適用する前にアーカイブするために送信された情報を、Commerce管理者で手動で復元する必要があります。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-8007\_EE\_2.2.0\_v1.composer.patch のダウンロード](assets/MDVA-8007_EE_2.2.0_v1.composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* Adobe Commerce 2.2.0

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* Adobe Commerce オンプレミス、Adobe Commerce on cloud infrastructure 2.2.1 - 2.2.3

## パッチの適用方法

手順については、を参照してください [Adobe Commerceが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。

## ユーザーガイドの便利なリンク

* [アーカイブ済み注文の管理](https://docs.magento.com/user-guide/sales/order-archive.html)

## 添付ファイル
