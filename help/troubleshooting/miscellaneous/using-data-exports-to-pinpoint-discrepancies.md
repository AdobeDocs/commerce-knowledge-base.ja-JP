---
title: データ書き出しの使用による不一致の特定
description: この記事では、Magentoの BI データの不一致をトラブルシューティングする方法について説明します。 データエクスポートは、特に [data dispensity diagnostic checklist] （https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy）で問題を特定できなかった場合に、レポートでデータの相違を特定するために、Magentoの BI データとソースデータを比較するのに便利なツールです。 この記事では、データ書き出しを使用してデータの不一致を特定する方法の実際の例について説明します。
exl-id: b42d585c-ad8c-4685-9ad4-a13686566f18
feature: Commerce Intelligence, Data Import/Export
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 0%

---

# データ書き出しの使用による不一致の特定

この記事では、Magentoの BI データの不一致をトラブルシューティングする方法について説明します。 データ書き出しは、特に [&#x200B; データの相違に関する診断チェックリスト &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy) が問題の特定に役立たなかった場合に、レポートのデータの相違を特定するために、Magentoの BI データとソースデータを比較するのに役立つツールです。 この記事では、データ書き出しを使用してデータの不一致を特定する方法の実際の例について説明します。

例えば、次の分析を考えてみましょう。

![](assets/Exports_Discrepancies_1.png)

2014 年 11 月は不審な下落が見られます。 500,780.94 ドルの収入？ そんな事言ってないよ。 ソースデータベースに、2014 年 11 月でより多くの売上高が表示されていることを確認し、このレポートで使用する **売上高** 指標が正しく定義されていることを再確認しました。 MagentoBI データウェアハウスのデータが不完全であり、データエクスポートを使用して確認できるようです。

## データのエクスポート {#export}

開始するには、グラフの右上隅にある歯車をクリックし、ドロップダウンメニューの「生の書き出し」オプションをクリックします。 これにより、グラフの背後にあるデータを生の形式で書き出すことができます。

![](assets/Export_Discrepancies_5.gif)

**生データの書き出し** メニューでは、書き出し元のテーブルと、書き出しに含める列を選択できます。 結果セットにフィルターを適用することもできます。

この例では、このレポートで使用される **売上高** 指標は、**`orders`** テーブルで定義された **order\_total** フィールド（**date** をタイムスタンプとして使用します。 この書き出しには、2014 年 11 月のすべての **order\_id** 値と、それらの **order\_total** を含めたいと思います。 **売上高** 指標ではフィルターを使用していませんが、書き出しにフィルターを追加して、結果セットを 2014 年 11 月のみに制限します。

生データの書き出しメニューは、次の例のようになります。

![](assets/Exports_Discrepancies_2.png)

「データの書き出し」をクリックして書き出しを開始します。 ステータスを含む書き出しの詳細を示すウィンドウが表示されます。 書き出しの準備には数分かかるので、**date、order\_id**、**order\_total** など、2014 年 11 月のソースデータの類似した抽出を実行するのに良い時間になります。 このファイルを Excel で開き、そのままにしておきます。このファイルについては後ほど説明します。

生データの書き出しウィンドウに「ダウンロード」ボタンが表示されたら、ボタンをクリックして、CSV ファイルを含む zip ファイルをダウンロードします。

![](assets/Export_Discrepancies_6.png)

この時点で、問題を見つけるためにすべてのデータを 1 つのシートに入れる必要があります。 CSV ファイル（Magento BI からの書き出し）を、ソースデータを含む Excel ファイルの別のシートに読み込みます。

## 問題の特定 {#pinpoint}

すべてのデータが 1 か所にまとまったので、相違の原因を探すことができます。 各シートの行数を比較すると、問題を特定するのに役立ちます。 それぞれの状況を詳しく見てみましょう。

### 両方のシートに含まれる行数は同じです

両方のシステムの行数が同じで、**売上高** 指標がソースデータに一致しない場合、**order\_total** はどこかでオフになっている必要があります。 **order\_total** フィールドがソースデータベースで更新されており、MagentoBI がこれらの変更を取得していない可能性があります。

これを確認するには、**order\_total** 列が再チェックされているかどうかを確認します。 Data Warehouseマネージャーに移動し、**`orders`** のテーブルをクリックします。 [&#x200B; 再確認頻度 &#x200B;](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/analyze/warehouse-manager/cfg-data-rechecks.html?lang=ja) が「変更」に表示されます。 列。 **order\_total** フィールドは、変更が予想される頻度で再チェックするように設定する必要があります。そうでない場合は、続行して、目的の再チェック頻度に設定します。

### ![](assets/Export_Discrepancies_4.gif)

再チェックの頻度が既に正しく設定されている場合は、別の問題が発生しています。 次の手順については、この記事の最後にある [&#x200B; サポートへのお問い合わせ &#x200B;](#support) を参照してください。

## ソース データベースの行数がMagento BI の行数を超えています {#morerows}

ソース・データベースにMagentoBI よりも多くの行があり、そのギャップが更新サイクル中に受け取ると予想されるオーダー数より大きい場合は、接続に問題がある可能性があります。 つまり、MagentoBI はソースデータベースから新しいデータを取り込むことができず、これはいくつかの理由で発生する可能性があります。

接続ページに移動し、`order` のテーブルを含むデータソースのステータスを確認します。

1. **ステータスが再認証の場合**、接続で正しい資格情報が使用されていません。 接続をクリックし、正しい資格情報を入力して、もう一度試してください。
1. **ステータスが失敗の場合**、接続がサーバー側で正しくセットアップされていない可能性があります。 通常、接続の失敗はホスト名が正しくないか、ターゲットサーバーが指定されたポートで接続を受け入れないために発生します。接続をクリックしてホスト名のつづりを再確認し、正しいポートが入力されていることを確認します。 サーバー側で、ポートが接続を受け入れ、ファイアウォールに許可されたMagentoBI IP アドレス（54.88.76.97/32）が設定されていることを確認します。 **接続が引き続き失敗する場合**、この記事の最後にある [&#x200B; サポートへのお問い合わせ &#x200B;](#support) の節を参照して、次の手順を確認してください。
1. **ステータスが成功の場合**、接続は問題ではないため、RJ サポートに協力する必要があります。 次の手順については、この記事の最後にある [&#x200B; サポートへのお問い合わせ &#x200B;](#support) を参照してください。

## ソース データベースの行数がMagento BI の行数より少なくなっています {#lessrows}

ソース・データベースの行数がMagentoBI の行数よりも少ない場合は、ソース・データベースから行が削除され、MagentoBI がこれらの削除を取得していない可能性があります。 **&#x200B; [&#x200B; データを削除 &#x200B;](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/best-practices/data/opt-db-analysis.html?lang=ja) すると、不一致、更新時間の延長、ロジスティック上の多くの問題につながる可能性があるので**&#x200B;本当に必要でない限り、データを削除しないことを強くお勧めします。

ただし、ローがテーブルから削除された場合は、プライマリ・キーの再チェック頻度を確認してください。 プライマリキーを再チェックすると、テーブルの削除された行がチェックされます。

Data Warehouseマネージャでは、主キー列はキーシンボルでマークされます。 この例では、プライマリキーは **order\_id** 列です。

![](assets/Export_Discrepancies_3.png)

プライマリキーが既に再チェックされるように設定されている場合、または行がこのテーブルから削除されない場合は、問題を特定するために RJ サポートが必要です。 次の手順については、次の節を参照してください。

## サポートへのお問い合わせ {#support}

問題の原因を特定できない場合は、RJ サポートでループする必要があります。 チケットを送信する前に、次の手順を実行してください。

* **ソースデータベースとMagentoBI の行数が同じで** 再確認の頻度が正しく設定されている場合、スプレッドシート **で VLOOKUP を実行して、MagentoBI とソースデータベースの間で order\_id の値が異なる order\_total を持つ値を見つけます。** チケットを送信する際に、これらの値を含めます。
* **ソースデータベースの行数が Connection BI の行数を超えており** Magentoが成功と表示されるか引き続き失敗する場合は、接続名と、表示されているエラーメッセージ（存在する場合）を把握する必要があります。
* **ソース・データベースの行がMagentoBI より少なく、** 行がテーブルから削除されず、かつ頻度が正しく設定されている場合は、スプレッドシートで VLOOKUP を実行して **どの order\_id 値がMagentoBI にあるのか** 確認しますが、ソース・データベースには存在しません。 チケットを送信する際に、これらの値を含めます。

## 関連資料

* [&#x200B; データ不整合の診断チェックリスト &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy)
* [Adobe Commerce Intelligence サービスポリシー &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies)
* Commerce実装プレイブックの [&#x200B; データベーステーブルを変更する際のベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)

