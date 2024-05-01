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

# 実行中に「市外局番が設定されていません」エラーが発生する `setup:upgrade`

この記事では、の取得に関連するAdobe Commerce on cloud infrastructure 2.2.3 の既知の問題に対するパッチを提供します *「市外局番が設定されていません」* 次のコマンドの実行中にエラーが発生しました：

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

コマンドを実行すると、次のエラーメッセージが表示されます。 *「モジュール「Magento\_AdvancedSalesRule」：データをインストール中…市外局番が設定されていません：セッションを開始する前に、市外局番を設定する必要があります」* コマンドの実行が中断されます。 この問題は、実際に設定される前にエリアの設定が要求されることが原因で発生します。 パッチを適用すると、エラーをキャッチでき、アップグレードプロセスが中断されることはありません。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-10439\_EE\_2.2.3\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-10439_EE_2.2.3_COMPOSER_v1.patch.zip)

## 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.2.3 上のAdobe Commerce

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.2.0 - 2.2.3

## パッチの適用方法

手順については、を参照してください [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。

## 添付ファイル
