---
title: Adobe Commerce上のクラスター内のvCPU層を表示する
promoted: true
description: この記事では、「Observation for Adobe Commerce」の「New Relic Infra」タブを使用して、vCPU層の割り当てを確認する方法について説明します。 Observation for Adobe Commerceは、New Relic サイトの状態、現在および過去の時間ビューを示すAdobe Commerce ナードレットです。
exl-id: a0332e7e-d38d-47d3-b3da-293902f45edc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%
---
# Adobe Commerce上のクラスター内のvCPU層を表示する

この記事では、「Observation for Adobe Commerce」の「New Relic Infra」タブを使用して、vCPU層の割り当てを確認する方法について説明します。 Observation for Adobe Commerceは、New Relic サイトの状態、現在および過去の時間ビューを示すAdobe Commerce ナードレットです。

## 影響を受ける製品とバージョン：

Adobe Commerce on cloud infrastructure 2.4.3 - 2.4.6

## Observation for Adobe CommerceでvCPU層の割り当てを確認します。

Adobe Commerce用New Relic Observationにアクセスしてログインするには、次の手順を実行します。

1. New Relicのホームページで、**アプリ**&#x200B;をクリックします。
1. Adobe Commerce **の**&#x200B;観察をクリックします。
1. Adobe Commerceのオナガメの観察が開きます。
1. 「**アカウントを選択**」ドロップダウンをクリックし、アカウントを選択します。
1. プロジェクト ID、New Relicのアカウント番号またはアカウント名を入力するか、アカウントのリストを参照できます。
1. 時計アイコン（nerdlet ウィンドウの右上）がある水色のドロップダウンメニューをクリックします。
1. イベント/イシューの原因を特定する場合は、チケットの日時の前の時間を選択して、先行するイベント/データがあるかどうかを確認します。 プリセット時間枠を使用するか、**カスタム設定**&#x200B;を選択してカスタム時間枠を設定できます。
1. タブで、**Infra**&#x200B;をクリックします。 vCPU層グラフは3つあります。
   * 最初のグラフには、2週間を超えるタイムラインの&#x200B;**vCPU階層ビューが表示されます（2週間を超えるタイムラインを選択する必要があります）。 注：サンプルレートは1日あたり。 1日にクラスターのアップサイズ/ダウンサイズが発生した場合、次の日**&#x200B;に終了階層サイズが表示されます。
   * 2番目のグラフは、タイムラインに対する&#x200B;**vCPU層ビューを示しています（24時間を超え、2週間未満のタイムラインを選択する必要があります）**。
   * 3つ目のグラフは、タイムライン BY ノードの&#x200B;**vCPU層ビューを示しています。タイムラインは24時間未満である必要があります**。
