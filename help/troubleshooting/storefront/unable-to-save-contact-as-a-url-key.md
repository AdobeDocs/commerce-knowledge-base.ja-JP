---
title: '*連絡先*を URL キーとして保存できません'
description: この記事では、製品または CMS ページの URL キー（例：「/contact」）として*contact*を保存できない場合の問題の回避策を説明します。 URL キーを保存しようとすると、URL キーが重複した URL であることを示すエラーが表示されます。
exl-id: eb340813-aba5-43a4-af5d-8fb64c93e021
feature: CMS, Marketing Tools, Storefront
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 保存できません *連絡先* URL キーとして

この記事では、保存できない場合の問題の回避策を説明します *連絡先* 製品または CMS ページの URL キー（「/contact」など）として使用します。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.x

## 問題

という用語を使用して製品または CMS ページを保存することはできません *連絡先* を URL キーとして使用します。 URL キーを保存しようとすると、URL キーが重複した URL であることを示すエラーが表示されます。

<u>再現手順</u>:

を使用した CMS ページの作成 *連絡先* を URL キーとして使用します。

<u>期待される結果</u>:

ページの保存先 *連絡先* を URL キーとして使用します。

<u>実際の結果</u>:

ページを保存することはできません。 次のエラーが発生します。 *「URL キー」フィールドに指定した値は、既に存在する URL を生成します。*

## 原因：

*連絡先* は、で定義された予約語です。 `vendor/magento/module-contact/view/frontend/layout/contact_index_index.xml`.

```xml
<router id="standard">
      <route id="contact" frontName="contact">
          <module name="Magento_Contact" />
      </route>
  </router>
```

## 解決策

この用語は使用できません *連絡先* ただし、URL キーとして、という用語を使用できます *連絡先* 別の文字または数字と組み合わせる（例： *連絡先 1* および *連絡先 2*）に設定します。 という用語は必須ではありませんが、 *連絡先+\&lt;another number=&quot;&quot; or=&quot;&quot; letter=&quot;&quot;>*&#x200B;の場合、長さが 255 文字を超えない限り、任意の文字列を指定できます。

次の手順を実行します。

1. Commerce管理者にログインします。
1. に移動 **[!UICONTROL Marketing]** > **[!UICONTROL SEO & Search]** > **[!UICONTROL URL Rewrites]**.
1. クリック **[!UICONTROL Add URL Rewrite]**.
1. を選択 *[!UICONTROL Custom]* 日 [!UICONTROL Create URL Rewrite] ドロップダウン。
   1. が含まれる [!UICONTROL Request Path]は、「連絡先」と入力します。 は [!UICONTROL Request Path] は、ユーザーがブラウザーおよび [!UICONTROL Target Path] は、リダイレクト先となる場所です。
   1. が含まれる [!UICONTROL Target Path]に入力し、新しい URL キーを入力します（例：「contact1」）。
   1. を選択 *[!UICONTROL No]* が含まれる [!UICONTROL Redirect] ドロップダウン。

## 関連資料

* [URL リライト](https://docs.magento.com/user-guide/marketing/url-rewrite.html) を参照してください。
* [SEO のベストプラクティス](https://docs.magento.com/user-guide/marketing/seo-best-practices.html) を参照してください。
