---
title: クラウドインフラストラクチャー上のAdobe Commerceに対するホリデーサージ容量リクエスト
description: ホリデーシーズンのピーク時（11 月中旬から 1 月中旬ごろ）には、Adobeでは、Adobe Commerceのすべてのマーチャントがクラウドインフラストラクチャでホストされ、トラフィックの増加に備えることをお勧めします。
exl-id: 9d6910bf-30bc-4117-bf7f-a0316f9506b5
feature: Cloud, Paas
role: Admin
source-git-commit: dfd3f788f42677b631ffb5b3153a1c79c2cc1ca3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceに対するホリデーサージ容量リクエスト

ホリデーシーズンのピーク時（11 月中旬から 1 月中旬ごろ）には、Adobeでは、Adobe Commerceのすべてのマーチャントがクラウドインフラストラクチャでホストされ、トラフィックの増加に備えることをお勧めします。

**トラフィックの計画と見積もり**

アドビのクラウドインフラストラクチャでは、すべてのAdobe Commerce マーチャントに対して以下をお勧めします [ピークシーズントラフィックの見積もり方法に関するこのレコメンデーションのセットを活用します](https://business.adobe.com/blog/how-to/the-5-ps-of-peak-season-performance-a-guide-to-preparing-your-infrastructure-for-high-traffic) 毎年ピークホリデーのセールスシーズンのために。

推奨される見積もりを完了した後、チームが追加容量が必要と感じる日付を特定した場合は、次のステップに進んで、追加容量の追加要求の方法に関する情報を確認してください。

**アップサイズの履歴の表示**

リクエストされたサイズ変更の履歴は、で確認できます [プロジェクトポータル（オンボーディング UI）](https://devdocs.magento.com/cloud/onboarding/onboarding-tasks.html)、の下 **プロジェクト** > **サービス** > **CPU 使用率のトラッキング**.
サイズ変更リクエストごとに、次の情報を使用できます。

* **サイズの開始日**：アップサイズリクエストの日付。
* **サイズ終了日**：クラスターが以前のサイズに戻された日付。
* **vCPU サイズ**：アップサイズ後のクラスターのサイズ。
* **使用日数**：クラスターがアップサイズされたままであった日数。
* **期間 vCPU**:vCPU サイズが使用日数によって変更されました。 （例えば、vCPU サイズ 192 x 25 日は 4,800 です）。

**サージ容量の要求**

ホリデーシーズン中に追加容量の必要性を予測するクラウドインフラストラクチャのAdobe Commerce マーチャントは、次のことを行う必要があります [サージ キャパシティ サポート チケットを送信する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html) を使用 [ヘルプセンター](/help/overview.md)日付と、チケット内での予想される処理能力のニーズを示します。 容量を増やすには、ライセンス済みの超過容量を使用する必要があります。

**これらのチケットは、容量が必要な場合の少なくとも 48 営業時間前に提出することをお勧めします。また、ブラックフライデー/サイバーマンデー期間の容量が制限されているので、可能な限り事前にリクエストを配置することをお勧めします。**


**ヘルプを表示する**

ピークシーズンのトラフィックに備えるために、より多くのガイダンスが必要ですか？ クラウドインフラストラクチャを利用するAdobe Commerceのマーチャントは、ピークシーズンを成功に導くためのヘルプ、戦略および計画に関するヒントについて、Adobeアカウントチームにお問い合わせください。 を確認することもお勧めします。 [Magentoブログ](https://magento.com/blog) 年間戦略のヒントに。

## 処理能力のレビューに関するリソース

サポートナレッジベースでは、

* [クラウド上のAdobe Commerceの CPU 割り当ての計算](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-cpu-allocation-calculation.html)
* [クラウド上のAdobe Commerceでホストのインスタンスのアップサイズが必要かどうかを確認する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-if-upsize-for-hosts-instances-is-needed.html)
* [クラウド上のAdobe Commerceに対するホストの CPU 設定の確認](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-hosts-cpu-configuration.html)
* [クラウド上のAdobe Commerceの停止の特定と測定](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-identify-outages.html)
