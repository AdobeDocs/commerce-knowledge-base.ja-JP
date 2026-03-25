---
title: setup:upgradeの実行中に「Area code is not set」エラーが発生する
description: この記事では、setup:upgrade コマンドを実行する際の*Area code is not set* エラーに関連する既知のAdobe Commerce on cloud infrastructure 2.2.3の問題に対するパッチを提供します。
exl-id: ace92331-6022-49fa-a776-d06d841b3b32
feature: Install, Upgrade
role: Developer
source-git-commit: 1dcd003bd9b08741c0fba464f5520797cfaeccbb
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# `setup:upgrade`の実行中に「市外局番が設定されていません」エラーが発生する

この記事では、次のコマンドを実行する際に&#x200B;*「市外局番が設定されていません」* エラーを取得することに関連する既知のAdobe Commerce on cloud infrastructure 2.2.3の問題に対するパッチを提供します。

```bash
setup:upgrade
```

>[!NOTE]
>
>この問題は、Adobe Commerce 2.2.4で修正されました。

## イシュー

を実行する場合

```bash
bin/magento setup:upgrade
```

コマンドを実行すると、次のエラーメッセージが表示されます。*「Module &#39;Magento\_AdvancedSalesRule&#39;: Installing data...Area code not set: Area code must be set before starting a session&quot;* and the command execution is interrupted. この問題は、実際に設定される前にエリア設定が要求されたために発生します。 パッチを適用すると、エラーを検出し、アップグレードプロセスを中断しないようにできます。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後までスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-10439\_EE\_2.2.3\_COMPOSER\_v1.patchをダウンロード](assets/MDVA-10439_EE_2.2.3_COMPOSER_v1.patch.zip)

## 互換性のあるAdobe Commerceのバージョン：

パッチは次の目的で作成されました。

* Adobe Commerce on cloud infrastructure 2.2.3

このパッチは、次のAdobe Commerce バージョンおよびエディションと互換性があります（ただし、問題が解決しない可能性があります）。

* Adobe Commerce on cloud infrastructureおよびAdobe Commerce on-premises 2.2.0 - 2.2.3

## パッチの適用方法

手順については、サポートナレッジベースの「[Adobeが提供するコンポーザーパッチを適用する方法](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/how-to-apply-a-composer-patch-provided-by-magento)」を参照してください。

## 添付ファイル
