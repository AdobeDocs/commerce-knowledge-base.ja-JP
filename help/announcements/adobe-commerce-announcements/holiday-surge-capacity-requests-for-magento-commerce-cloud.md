---
title: クラウドインフラストラクチャー上のAdobe Commerceに対するホリデーサージ容量リクエスト
description: ホリデーシーズンのピーク時（11 月中旬から 1 月中旬ごろ）には、Adobeでは、Adobe Commerceのすべてのマーチャントがクラウドインフラストラクチャでホストされ、トラフィックの増加に備えることをお勧めします。
exl-id: 9d6910bf-30bc-4117-bf7f-a0316f9506b5
feature: Cloud, Paas
role: Admin
source-git-commit: 357e0acb1c849079ff0fe9f53fe386f60475c7f9
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceに対するホリデーサージ容量リクエスト

ホリデーシーズンのピーク時（11 月中旬から 1 月中旬ごろ）には、Adobeでは、Adobe Commerceのすべてのマーチャントがクラウドインフラストラクチャでホストされ、トラフィックの増加に備えることをお勧めします。

**トラフィックの計画と見積もり**

毎年、ホリデーのピークセールスシーズンに備えて、クラウドインフラストラクチャ上のすべてのAdobe Commerce マーチャントに [&#x200B; このレコメンデーションのセットを利用してピークシーズントラフィックを見積もる方法 &#x200B;](https://business.adobe.com/blog/how-to/the-5-ps-of-peak-season-performance-a-guide-to-preparing-your-infrastructure-for-high-traffic) をお勧めします。

推奨される見積もりを完了した後、チームが追加容量が必要と感じる日付を特定した場合は、次のステップに進んで、追加容量の追加要求の方法に関する情報を確認してください。

**アップサイズの履歴を表示**

**CSM （Customer Success Manager）** に情報を要求すると、要求されたサイズ変更の履歴を表示できます。
サイズ変更リクエストごとに、次の情報を使用できます。

* **サイズ開始日**：アップサイズリクエストの日付。
* **サイズ終了日**：クラスターが以前のサイズに戻された日付。
* **vCPU サイズ**：アップサイズ後のクラスターのサイズです。
* **使用日数**：クラスターがアップサイズのままであった日数。
* **期間 vCPU**:vCPU サイズが使用日数だけ変更されました。 （例えば、vCPU サイズ 192 x 25 日は 4,800 です）。

**サージ容量の要求**

ホリデーシーズン中に追加の容量の必要性を予測するクラウドインフラストラクチャ上のAdobe Commerce マーチャントは、日付とチケット内の予想される容量のニーズを示す [Surge Capacity Support Ticket を送信 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html?lang=ja) するには、[&#x200B; ヘルプセンター &#x200B;](/help/overview.md) を使用します。 容量を増やすには、ライセンス済みの超過容量を使用する必要があります。

**これらのチケットは、定員が必要な場合は 48 営業時間前までに提出することをお勧めします。また、ブラックフライデー/サイバーマンデー期間の定員が限られているため、可能な限り事前にリクエストすることをお勧めします。**


**その他のヘルプ**

ピークシーズンのトラフィックに備えるために、より多くのガイダンスが必要ですか？ クラウドインフラストラクチャを利用するAdobe Commerceのマーチャントは、ピークシーズンを成功に導くためのヘルプ、戦略および計画に関するヒントについて、Adobeアカウントチームにお問い合わせください。 また、年間を通じて戦略のヒントを紹介する [Magentoブログ &#x200B;](https://magento.com/blog) もチェックすることをお勧めします。

## 処理能力のレビューに関するリソース

サポートナレッジベースでは、

* [Cloud 上のAdobe Commerceの CPU 割り当ての計算 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-cpu-allocation-calculation.html?lang=ja)
* [Cloud 上のAdobe Commerceでホストのインスタンスのアップサイズが必要かどうかを確認する &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-if-upsize-for-hosts-instances-is-needed.html?lang=ja)
* [&#x200B; クラウド上のAdobe Commerceでホストの CPU 設定を確認する &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-hosts-cpu-configuration.html?lang=ja)
* [Cloud 上のAdobe Commerceの停止の特定と測定 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-identify-outages.html?lang=ja)
