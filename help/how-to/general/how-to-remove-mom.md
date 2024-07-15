---
title: Magento Order Management（MOM）の削除方法
description: この文書では、Magento Order Management（MOM）システムを取り外す方法について説明します。
exl-id: 9b2adb30-a880-45a2-859e-be0da42bfd07
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Magento Order Management（MOM）の削除方法

1. [ 統合の無効化または有効化 ](/docs/commerce-admin/systems/integrations/mcom.html#disable-or-enable-the-integration) の手順に従って、MOM 統合を無効にします。
1. [ モジュールのアンインストール ](/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html) の手順に従って、MOM モジュールを無効にします。
1. フルオーダーデータを抽出するには、API を提供しています。 詳しくは、Adobeの [ 注文リポジトリー ](https://omsdocs.magento.com/specifications/#magento.sales.order_repository) を確認してください |注文情報（order_repository）をカバーするMagentoOMS ドキュメント。 Adobeで [ 仕様セクション ](https://omsdocs.magento.com/specifications/#services) を使用します。 | Magento他の API を使用して様々な情報タイプを抽出するための OMS ドキュメント。
