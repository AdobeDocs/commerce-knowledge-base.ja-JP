---
title: 「setup:upgrade の実行中に「市外局番が設定されていません」エラーが発生する」
description: この文書では、setup:upgrade コマンドの実行時に発生する*Area code is not set* エラーに関連する、Adobe Commerce on cloud infrastructure 2.2.3 の既知の問題に対するパッチを提供します。
exl-id: ace92331-6022-49fa-a776-d06d841b3b32
feature: Install, Upgrade
role: Developer
source-git-commit: 4617b915a62093e00da428a753d913a39d30f3a0
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# `setup:upgrade` を実行中に「市外局番が設定されていません」エラーが発生する

この記事では、次のコマンドを実行した際に *エリアコードが設定されていません」というエラーが発生することに関連する* Cloud Infrastructure 2.2.3 上の既知のAdobe Commerceの問題に対するパッチを提供します。

```bash
setup:upgrade
```

>[!NOTE]
>
>この問題は、Adobe Commerce 2.2.4 で修正されました。

## 問題

を実行するとき

```bash
bin/magento setup:upgrade
```

Magento コマンドで「*Module &#39;Module\_AdvancedSalesRule&#39;: Installing data...Area code not set: Area code must set before a session」というエラーメッセージが表示され* コマンドの実行が中断されます。 この問題は、実際に設定される前にエリアの設定が要求されることが原因で発生します。 パッチを適用すると、エラーをキャッチでき、アップグレードプロセスが中断されることはありません。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-10439\_EE\_2.2.3\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-10439_EE_2.2.3_COMPOSER_v1.patch.zip)

## 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.2.3 上のAdobe Commerce

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.2.0 - 2.2.3

## パッチの適用方法

手順については、サポートナレッジベースの [Adobe提供の Composer パッチの適用方法 &#x200B;](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 添付ファイル
