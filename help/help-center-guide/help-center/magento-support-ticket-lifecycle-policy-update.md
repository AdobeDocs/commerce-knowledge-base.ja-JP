---
title: Adobe Commerce サポートチケットのライフサイクルポリシーの更新
description: この記事では、Adobe Commerce サポートチケットライフサイクルポリシーの更新に関する情報を提供します。
exl-id: c3fbcb4a-107f-48b3-afed-b9a0c5d0425c
source-git-commit: c1c2bd29e14f4cbfffb235801e95ec7cbb7c7a55
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---

# Adobe Commerce サポートチケットのライフサイクルポリシーの更新

この記事では、Adobe Commerce サポートチケットライフサイクルポリシーの更新に関する情報を提供します。

次の表に、更新されたシナリオを示します。 各シナリオの詳細については、以下の節を参照してください。

<table>
 <tbody>
 <tr>
 <td class="wysiwyg-text-align-center"> </td>
 <td class="wysiwyg-text-align-center"><strong>チケットステータス</strong></td>
 <td class="wysiwyg-text-align-center"><strong>日数を「解決済み」に</strong></td>
 <td class="wysiwyg-text-align-center"><strong>日数から"クローズ"まで</strong></td>
 <td class="wysiwyg-text-align-center"><strong>通知のタイミング</strong></td>
 </tr>
 <tr>
 <td class="wysiwyg-text-align-left"><strong>エンジニアがソリューションを提供</strong></td>
 <td class="wysiwyg-text-align-center">"返信待ち"</td>
 <td class="wysiwyg-text-align-center">3</td>
 <td class="wysiwyg-text-align-center">6</td>
 <td class="wysiwyg-text-align-center">3 日目と 6 日目</td>
 </tr>
 <tr>
 <td class="wysiwyg-text-align-left"><strong>顧客からの情報待ち</strong></td>
 <td class="wysiwyg-text-align-center">"返信待ち"</td>
 <td class="wysiwyg-text-align-center">該当なし</td>
 <td class="wysiwyg-text-align-center">6</td>
 <td class="wysiwyg-text-align-center">1 日目、3 日目、6 日目</td>
 </tr>
 <tr>
 <td class="wysiwyg-text-align-left"><strong>顧客が「解決済み」に設定しているか、エンジニアに「解決済み」への設定をリクエストしている</strong></td>
 <td class="wysiwyg-text-align-center">「解決済み」</td>
 <td class="wysiwyg-text-align-center">即時</td>
 <td class="wysiwyg-text-align-center">1</td>
 <td class="wysiwyg-text-align-center">1 日目</td>
 </tr>
 </tbody>
 </table>

## シナリオの詳細

### エンジニアがソリューションを提供する場合

1. お客様に解決策が提供されると、エンジニアはチケットのステータスを「返信待ち」に設定します。
1. ステータスが「返信待ち」に変更された後、お客様からの応答がない場合は、チケットが「解決済み」に移動され、お客様に通知されます。
1. ステータスが「返信待ち」に変更されてから 6 日間、顧客からの応答がない場合 – チケットはクローズされ、顧客に通知されます。

### お客様から追加情報が必要な場合

1. 顧客からの更新が必要な場合、エンジニアはチケットを「返信待ち」に設定します。
1. 1 日目と 3 日目に、お客様にフォローアップを依頼する通知が送信されます。
1. ステータスが「返信待ち」に変更されてから 6 日間、顧客からの応答がない場合 – チケットはクローズされ、顧客に通知されます。

### 顧客によって「解決済み」に設定されたチケット

お客様がチケットを「解決済み」に設定すると、1 日でクローズし、お客様に通知されます。

### お客様がサポートに対してチケットをクローズするよう指示

お客様がAdobe Commerce サポートにチケットをクローズするように指示すると、1 日でクローズされ、お客様に通知されます。

## 関連資料

* [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)
* [Adobe Commerce ヘルプセンターの開始ページに「チケットを送信」リンクが表示されない](/help/help-center-guide/help-center/magento-help-center-user-guide.md#no-submit-link)
* [チケット送信フォーム：組織ドロップダウンにマーチャントが表示されない](/help/help-center-guide/help-center/magento-help-center-user-guide.md#merchant-not-displayed)
