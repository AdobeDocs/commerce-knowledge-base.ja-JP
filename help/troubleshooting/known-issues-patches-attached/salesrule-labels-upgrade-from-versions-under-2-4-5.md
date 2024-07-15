---
title: バージョン < 2.4.5**のアップグレード時の「**[!UICONTROL salesRules]」ラベルの問題
description: Adobe Commerce バージョン 2.4.5 より前のバージョンからアップグレードする場合は、**[!UICONTROL salesRules]**の問題に対処するためのパッチを適用します。
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# バージョン &lt; 2.4.5 からアップグレードする場合の **[!UICONTROL salesRules]** ラベルの問題

**[!UICONTROL salesRules]** ラベルのステージング機能は、Adobe Commerce [2.4.5](/docs/commerce-operations/release/notes/adobe-commerce/2-4-5.html) で導入されました。 この変更により、Adobe Commerce &lt; 2.4.5 から任意のバージョン >= 2.4.5 にアップグレードする際に問題が発生する可能性があります。アップグレード後、ラベルが一致 **[!UICONTROL salesRules]** ない可能性があります。 この問題に対処するには、新しいAdobe Commerce バージョンへのアップグレード直後にパッチを適用する必要があります。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce &lt; 2.4.5

## パッチ

次の添付パッチを使用します。

[ACSD-50625_2.4.5-P1.patch.zip](assets/ACSD-50625_2.4.5-p1.patch.zip)

## パッチの適用方法

1. Commerce ガイドの [ アップグレードを実行する ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade.html) の手順に従います。
1. **[!UICONTROL Update metadata]** フェーズの前に、添付のパッチを適用します。
（**[!UICONTROL Update metadata]** フェーズが完了した後にパッチを適用することもできますが、その場合は `bin/magento setup:upgrade` を再度実行する必要があります）。
1. [ アップグレードの実行 ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade.html) の残りの手順に進みます。
