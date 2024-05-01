---
title: '''**[!UICONTROL salesRules]バージョン < 2.4.5''からアップグレードする際の** ラベルの問題'
description: その**に対処するためにパッチを適用する[!UICONTROL salesRules]Adobe Commerce バージョン 2.4.5 より前のバージョンからアップグレードする場合の**の問題。
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# **[!UICONTROL salesRules]** バージョン &lt; 2.4.5 からアップグレードする場合のラベルの問題

この **[!UICONTROL salesRules]** ラベルのステージング機能がAdobe Commerceに導入されました [2.4.5](/docs/commerce-operations/release/notes/adobe-commerce/2-4-5.html). この変更により、Adobe Commerce &lt; 2.4.5 から任意のバージョン >= 2.4.5 にアップグレードする際に問題が発生する可能性があります。アップグレード後、次の問題が発生する可能性があります **[!UICONTROL salesRules]** ラベルが一致しません。 この問題に対処するには、新しいAdobe Commerce バージョンへのアップグレード直後にパッチを適用する必要があります。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce &lt; 2.4.5

## パッチ

次の添付パッチを使用します。

[ACSD-50625_2.4.5-P1.patch.zip](assets/ACSD-50625_2.4.5-p1.patch.zip)

## パッチの適用方法

1. の手順に従います [アップグレードの実行](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade.html) Commerce ガイドをご覧ください。
1. を適用する前に、添付のパッチを適用してください **[!UICONTROL Update metadata]** フェーズ。
（パッチは、 **[!UICONTROL Update metadata]** フェーズで実行する必要がある `bin/magento setup:upgrade` もう一度）。
1. 残りの手順を次の中で続行します [アップグレードの実行](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade.html).
