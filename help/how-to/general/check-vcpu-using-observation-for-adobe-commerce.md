---
title: Adobe Commerce上のクラスターの環境 vCPU 層の表示
promoted: true
description: この記事では、Adobe Commerceの監視の「New Relicインフラストラクチャ」タブを使用して vCPU 層の割り当てを確認する方法を説明します。 Adobe Commerceの監視は、New Relic サイトの状況や現在および過去の時間表示を示すAdobe Commerce ナルレットです。
exl-id: a0332e7e-d38d-47d3-b3da-293902f45edc
source-git-commit: 309fda5284de3b8be54e95bf2bfd8ff1777b6c90
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Adobe Commerce上のクラスターの環境 vCPU 層の表示

この記事では、Adobe Commerceの監視の「New Relicインフラストラクチャ」タブを使用して vCPU 層の割り当てを確認する方法を説明します。 Adobe Commerceの監視は、New Relic サイトの状況や現在および過去の時間表示を示すAdobe Commerce ナルレットです。

## 影響を受ける製品とバージョン：

クラウドインフラストラクチャー上のAdobe Commerce 2.4.3 - 2.4.6

## Adobe Commerceの監視を使用して vCPU 層の割り当てを確認します。

New Relic Observation for Adobe Commerceのサーブレットにアクセスしてログインするには：

1. New Relicのホームページで、「**アプリ**」をクリックします。
1. **Adobe Commerceの監視** をクリックします。
1. 「Adobe Commerceの監視」サーブレットが開きます。
1. **アカウントを選択** ドロップダウンをクリックし、アカウントを選択します。
1. プロジェクト ID、New Relicのアカウント番号またはアカウント名を入力したり、アカウントのリストを参照したりできます。
1. 時計アイコンが表示されている水色のドロップダウンメニュー（ネルレットウィンドウの右上）をクリックします。
1. イベント/問題の原因を特定しようとしている場合は、チケットの日時より前の時間を選択して、先行するイベント/データがあるかどうかを確認します。 プリセットされた時間枠を使用するか、「**カスタムを設定**」を選択してカスタムの時間枠を設定できます。
1. タブで [**インフラストラクチャ**] をクリックします。 vCPU 階層のグラフは次の 3 つです。
   * 最初のグラフは、2 週間を超えるタイムラインの **vCPU 層の表示を示しています（2 週間を超えるタイムラインを選択する必要があります）。 メモ：サンプルレートは 1 日ごとになります。 クラスターのアップサイズ/ダウンサイズが 1 日で発生した場合、終了層のサイズは翌日** に表示されます。
   * 2 つ目のグラフは、タイムラインの **vCPU 層のビューを示しています（24 時間を超え 2 週間以内のタイムラインを選択する必要があります）**。
   * 3 番目のグラフは、ノード別のタイムラインの **vCPU 層ビューを示しています。24 時間未満のタイムラインを見る必要があります**。

## 関連資料

* [Adobe Commerceの概要の確認 ](/help/support-tools/observation-for-adobe-commerce/observation-adobe-commerce-overview.md) をサポートナレッジベースで行います。
