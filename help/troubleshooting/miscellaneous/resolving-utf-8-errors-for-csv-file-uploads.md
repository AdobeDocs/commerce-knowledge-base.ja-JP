---
title: CSV ファイルアップロードに関する UTF-8 エラーの解決
description: この記事では、「CSV ファイルは UTF-8 エンコーディングを使用する必要があります」というエラーメッセージが表示された場合の修正方法を説明します。 このエラーメッセージは、アップロードしようとしているファイルに無効な文字が含まれているか、許可されていない文字が含まれていることを意味します。 UTF-8 エンコーディングでは [ 大部分の文字 ] （https://www.fileformat.info/info/charset/UTF-8/list.htm）が可能ですが、Magento BI と互換性がないものもあります。
exl-id: 88d8e0b8-152e-4a6d-bc44-3b285e0eb0c3
feature: Data Import/Export
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# CSV ファイルアップロードに関する UTF-8 エラーの解決

この記事では、「CSV ファイルは UTF-8 エンコーディングを使用する必要があります」というエラーメッセージが表示された場合の修正方法を説明します。 このエラーメッセージは、アップロードしようとしているファイルに無効な文字が含まれているか、許可されていない文字が含まれていることを意味します。 UTF-8 エンコーディングではを使用できます。 [登場人物の大半](https://www.fileformat.info/info/charset/UTF-8/list.htm)、一部はMagento BI と互換性がありません。

この問題を修正するには、ファイルのエンコーディングを変更する必要があります。 通常、適切なエンコーディングでファイルを再保存すると問題は解決しますが、この操作を行うと、一部の情報（無効な文字が削除される場合など）が失われる可能性があることに注意してください。

を使用することをお勧めします。 [Sublime Text](https://www.sublimetext.com/2) ファイルを保存してエンコードします。

1. ファイルをMicrosoft Excel、Google ドキュメント、Apple番号、または選択したプログラムで開きます。
1. &#x200B;をクリック&#x200B; **ファイル** > **名前を付けて保存** &#x200B;&#x200B;&#x200B;の&#x200B;を選択します。 **コンマ区切り値（.csv）** ファイルを保存する形式。
1. Sublime Text で CSV ファイルを開きます。
1. Sublime Text で、&#x200B;の場所に移動し&#x200B;す。 **ファイル** > **エンコードを付けて保存** > **UTF-8\*&#x200B;** . これにより、UTF-8 エンコーディングで CSV ファイルが保存されます。    ![csv_file_UTF-8_sublime_3.2.2_magento_BI.png](assets/csv_file_UTF-8_sublime_3.2.2_magento_BI.png)
1. [データをアップロード](https://docs.magento.com/mbi/data-analyst/importing-data/connecting-data/using-file-uploader.html) （ユーザーガイドの）MagentoBI の新しいテーブルへ。
