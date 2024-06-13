---
title: 非推奨（廃止予定）のGoogleのイメージチャートをイメージチャートに置き換える
description: 現在、ほとんどのAdobe Commerceのエディションとバージョンでは、管理ダッシュボードで静的なグラフをレンダリングするために、[Google画像グラフ ] （https://developers.google.com/chart/image/）を使用しています。 2019 年 3 月 14 日（PT）をもって、GoogleはGoogle イメージチャートのサポートを停止します。 この問題を解決するために、Googleの画像チャートを [Image-Charts] （https://www.image-charts.com/）のフリーサービスに置き換えるパッチを提供しています。
exl-id: f86f0bb9-8a03-471d-8696-1eba4b8acbd1
feature: Cache, Compliance
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 非推奨（廃止予定）のGoogleのイメージチャートをイメージチャートに置き換える

現在、ほとんどのAdobe Commerce エディションとバージョンでを使用しています [Google画像グラフ](https://developers.google.com/chart/image/) 管理ダッシュボードで静的グラフをレンダリングする。 2019 年 3 月 14 日（PT）をもって、GoogleはGoogle イメージチャートのサポートを停止します。 この問題を解決するために、Google画像グラフをで置き換えるパッチを提供しています [Image-Chart](https://www.image-charts.com/) 無料サービス。

## 影響を受けるバージョン

* Adobe Commerce 1.X、すべてのエディション
* Adobe Commerce 2.X、すべてのエディション

>[!NOTE]
>
>Adobe Commerce オンプレミス 1.14.4.1、Magento Open Source 1.9.4.1、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.2 には、このグラフの更新が含まれます。 これらのバージョンにアップグレードすると、追加のパッチを適用しないイメージチャートが引き続きサポートされます。

## 問題

Googleは、2019 年 3 月 14 日（PT）をもって、Google イメージチャートのサポートを終了しました。 Adobe Commerce 1.X およびAdobe Commerce 2.2.X を使用する場合は、パッチをダウンロードして適用しない限り、静的なグラフを表示できません。Googleの画像グラフを画像グラフソリューションに置き換えてください。 表示されるグラフは、と同じデザインと機能を持ちます。Google画像グラフは、 [GDPR](https://www.image-charts.com/data-processing-addendum.html) コンプライアンスプライバシーポリシー。 その他のオプションについては、を参照してください。 [Image-Chart](https://www.image-charts.com/).

## 解決策

Commerce管理者で静的グラフを表示できるようにするには、Adobe Commerceから提供されるパッチをダウンロードして適用します。 追加の設定は必要ありません。

### Adobe Commerce オンプレミス

1. を保存します [attached MAGETWO-98833\_composer\_patch-2019-04-15-04-38-57.patch](assets/MAGETWO-98833_composer_patch-2019-04-15-04-38-57.patch.zip) パッチを適用して、Adobe Commerce ルートディレクトリにアップロードします。
1. パッチ名を実際のパッチ名に置き換えて、次の SSH コマンドを実行します。

   ```git
   patch -p1 < MAGETWO-98833_composer_patch-2019-04-15-04-38-57.patch
   ```

   上記のコマンドが機能しない場合は、を使用してみてください。 `-p2` の代わりに `-p1`.）

1. 変更を反映するには、の管理画面でキャッシュを更新します。 **システム** > **キャッシュ管理**.

### クラウドインフラストラクチャー上のAdobe Commerce

Cloud マーチャントの場合、パッチは最も近い ECE ツールのアップデートに含まれます。

### Magento2 オープンソース

1. に移動 [https://magento.com/tech-resources/download\#download2291](https://magento.com/tech-resources/download#download2291).
1. が含まれる **形式を選択** ドロップダウン リストから composer のバージョンを選択し、 **Download**.
1. パッチをAdobe Commerceのルートディレクトリにアップロードします。
1. パッチ名を実際のパッチ名に置き換えて、次の SSH コマンドを実行します。

   ```git
   patch -p1 < MAGETWO-98833_composer_patch-2019-04-15-04-37-48.patch
   ```

   （上記のコマンドが機能しない場合は、を使用してみてください。 `-p2` の代わりに `-p1`.）

1. 変更を反映するには、の管理画面でキャッシュを更新します。 **システム** > **キャッシュ管理**.

### Adobe Commerce 1 オンプレミス

次の手順に従って、パッチをダウンロードして適用します。

1. を保存します [添付 MPERF-10509-EE-2019-03-13-06-32-19.diff](assets/MPERF-10509-EE-2019-03-13-06-32-19.diff.zip) パッチを適用して、Adobe Commerce ルートディレクトリにアップロードします。
1. 次の SSH コマンドを実行します。

   ```git
   patch -p1 < MPERF-10509-EE-2019-03-13-06-32-19.diff
   ```

   （上記のコマンドが機能しない場合は、を使用してみてください。 `-p2` の代わりに `-p1`.）

1. 変更を反映するには、の管理画面でキャッシュを更新します。 **システム** > **キャッシュ管理**.

### Magento 1 オープンソース

次の手順に従って、パッチをダウンロードして適用します。

1. クリック [**このリンク**](https://magento.com/tech-resources/download#download2283) 管理ダッシュボードチャート パッチを探すには、次の手順に従います。
1. を選択

   ```git
   MPERF-10509.diff
   ```

   から **形式を選択** ドロップダウンで「ダウンロード」をクリックします。

1. Adobe Commerceのルートディレクトリにファイルをアップロードします。
1. 次の SSH コマンドを実行します。

   ```git
   patch -p1 < MPERF-10509.diff
   ```

   （上記のコマンドが機能しない場合は、を使用してみてください。 `-p2` の代わりに `-p1`.）

1. 変更を反映するには、の管理画面でキャッシュを更新します。 **システム** > **キャッシュ管理**.

## 添付ファイル

[MAGETWO-98833_composer_patch-2019-04-15-04-38-57.patch をダウンロード](assets/MAGETWO-98833_composer_patch-2019-04-15-04-38-57.patch)

[MPERF-10509-EE-2019-03-13-06-32-19.diffh のダウンロード](assets/MPERF-10509-EE-2019-03-13-06-32-19.diff)
