---
title: 管理者で一括削除中に、開始されたよりも多くの製品が削除されました
description: この記事では、Commerce Admin で一括削除がグリッド内で実行された場合に、選択したレコードが削除されないことに関連する、AdobeсCloud Infrastructure 2.2.3 上の既知の Commerce に対するパッチを提供します。
exl-id: 0bfdc84e-0292-4702-a20e-bdbe67c111a2
feature: Admin Workspace, Products
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# 管理者で一括削除中に、開始されたよりも多くの製品が削除されました

この記事では、Commerce Admin で一括削除がグリッド内で実行された場合に、選択したレコードが削除されないことに関連する、AdobeсCloud Infrastructure 2.2.3 上の既知の Commerce に対するパッチを提供します。

## 問題

管理者で、削除する顧客レコードまたはクライアントレコードを選択し、グリッドをフィルタリングしてから、**削除** アクションを選択すると、すべてのレコードが削除されます。

<u> 再現手順 </u>:

1. 管理で **カタログ**/**製品** に移動します。
1. 1 つまたは複数の製品を選択します。
1. アクション ドロップダウンメニューから「削除」を選択します。

<u> 期待される結果 </u>:

選択した製品のみが削除されます。

<u> 実際の結果 </u>:

その他の製品も同様に削除されます。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-10600\_EE\_2.2.3\_v1.composer.patch のダウンロード](assets/MDVA-10600_EE_2.2.3_v1.composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.2.3 上のAdobe Commerce

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* Adobe Commerce オンプレミス 2.1.8-2.1.14、2.2.0-2.2.2 および 2.2.4-2.2.5
* クラウドインフラストラクチャー上のAdobe Commerce 2.2.4-2.2.5

## パッチの適用方法

手順については、[Adobe Commerceが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。
