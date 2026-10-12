---
title: Magento Order Management （MOM）の削除方法
description: この記事では、Magento Order Management （MOM）システムを削除する方法について説明します。
exl-id: 9b2adb30-a880-45a2-859e-be0da42bfd07
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%
---
# Magento Order Management （MOM）の削除方法

1. [統合を無効にするか有効にする](https://commerce-docs.github.io/oms-documentation-archive/integration/connector/#disable-or-enable-the-integration)の手順に従って、MOM統合を無効にします。
1. [&#x200B; モジュールのアンインストール &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html)の手順に従って、MOM モジュールを無効にします。
1. フルオーダーデータを抽出するには、APIを提供しています。 詳しくは、注文情報（order_repository）をカバーするAdobe | Magento OMS Docsの[注文リポジトリ &#x200B;](https://commerce-docs.github.io/oms-documentation-archive/specifications/#magento.sales.order_repository)を確認してください。 Adobe | Magento OMS Docsの[仕様セクション &#x200B;](https://commerce-docs.github.io/oms-documentation-archive/specifications/#services)を使用すると、他のAPIを使用して様々な情報タイプを抽出できます。
