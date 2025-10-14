---
title: Magento Order Management（MOM）の削除方法
description: この文書では、Magento Order Management（MOM）システムを取り外す方法について説明します。
exl-id: 9b2adb30-a880-45a2-859e-be0da42bfd07
source-git-commit: 77f41d6034f985794e5c5b89cc007a69858683b9
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Magento Order Management（MOM）の削除方法

1. [&#x200B; 統合の無効化または有効化 &#x200B;](https://commerce-docs.github.io/oms-documentation-archive/integration/connector/#disable-or-enable-the-integration) の手順に従って、MOM 統合を無効にします。
1. [&#x200B; モジュールのアンインストール &#x200B;](/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html) の手順に従って、MOM モジュールを無効にします。
1. フルオーダーデータを抽出するには、API を提供しています。 詳しくは、Adobeの [&#x200B; 注文リポジトリー &#x200B;](https://commerce-docs.github.io/oms-documentation-archive/specifications/#magento.sales.order_repository) を確認してください |注文情報（order_repository）をカバーするMagentoOMS ドキュメント。 Adobeで [&#x200B; 仕様セクション &#x200B;](https://commerce-docs.github.io/oms-documentation-archive/specifications/#services) を使用します。 | Magento他の API を使用して様々な情報タイプを抽出するための OMS ドキュメント。
