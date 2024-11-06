---
title: CSV ファイルアップロードに関する UTF-8 エラーの解決
description: この記事では、「CSV ファイルは UTF-8 エンコーディングを使用する必要があります」というエラーメッセージが表示された場合の修正方法を説明します。 このエラーメッセージは、アップロードしようとしているファイルに無効な文字が含まれているか、許可されていない文字が含まれていることを意味します。 UTF-8 エンコーディングでは [ 大部分の文字 ] （https://www.fileformat.info/info/charset/UTF-8/list.htm）が可能ですが、Magento BI と互換性がないものもあります。
exl-id: 88d8e0b8-152e-4a6d-bc44-3b285e0eb0c3
feature: Data Import/Export
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# CSV ファイルアップロードに関する UTF-8 エラーの解決

この記事では、「CSV ファイルは UTF-8 エンコーディングを使用する必要があります」というエラーメッセージが表示された場合の修正方法を説明します。 このエラーメッセージは、アップロードしようとしているファイルに無効な文字が含まれているか、許可されていない文字が含まれていることを意味します。 UTF-8 エンコーディングでは [ 大部分の文字 ](https://www.fileformat.info/info/charset/UTF-8/list.htm) が可能ですが、Magento BI と互換性がないものもあります。

この問題を修正するには、ファイルのエンコーディングを変更する必要があります。 通常、適切なエンコーディングでファイルを再保存すると問題は解決しますが、この操作を行うと、一部の情報（無効な文字が削除される場合など）が失われる可能性があることに注意してください。

ファイルを保存してエンコードするには、[ 昇華テキスト ](https://www.sublimetext.com/2) を使用することをお勧めします。

1. ファイルをMicrosoft Excel、Google ドキュメント、Apple番号、または選択したプログラムで開きます。
1. &#x200B;&#x200B;**ファイル**/**名前を付けて保存**&#x200B;をクリックし&#x200B;&#x200B;&#x200B;**コンマ区切り値（.csv）** 形式を選択してファイルを保存します。
1. Sublime Text で CSV ファイルを開きます。
1. Sublime Text で&#x200B;&#x200B; **File**/**Save with Encoding**/**UTF-8\*&#x200B;** に移動します。 これにより、UTF-8 エンコーディングで CSV ファイルが保存されます。    ![csv_file_UTF-8_sublime_3.2.2_magento_BI.png](assets/csv_file_UTF-8_sublime_3.2.2_magento_BI.png)
1. ユーザーガイドの [ データをアップロード ](https://experienceleague.adobe.com/en/docs/commerce-business-intelligence/mbi/analyze/connecting/using-file-uploader) して、MagentoBI の新しいテーブルに貼り付けます。
