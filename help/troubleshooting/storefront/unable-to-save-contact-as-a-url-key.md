---
title: '*連絡先*を URL キーとして保存できません'
description: ここでは、商品やCMSページの URL キー（例：「/contact」）として*contact*を保存できない場合の対処法を示します。 URL キーを保存しようとすると、URL キーが重複した URL であることを示すエラーが表示されます。
exl-id: eb340813-aba5-43a4-af5d-8fb64c93e021
feature: CMS, Marketing Tools, Storefront
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# *連絡先* を URL キーとして保存できません

ここでは、商品またはCMSページの URL キーとして *contact* を保存できない場合の対処法を示します。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.x

## 問題

URL キーとして *連絡先* という用語を使用して、商品またはCMSページを保存することはできません。 URL キーを保存しようとすると、URL キーが重複した URL であることを示すエラーが表示されます。

<u> 再現手順 </u>:

*連絡先* を URL キーとして使用してCMS ページを作成します。

<u> 期待される結果 </u>:

ページは、URL キーとして *連絡先* と共に保存されます。

<u> 実際の結果 </u>:

ページを保存することはできません。 次のエラーが表示されます。*「URL キー」フィールドに指定された値は、既に存在する URL を生成します。*

## 原因：

*Contact* は、`vendor/magento/module-contact/view/frontend/layout/contact_index_index.xml` で定義された予約語です。

```xml
<router id="standard">
      <route id="contact" frontName="contact">
          <module name="Magento_Contact" />
      </route>
  </router>
```

## 解決策

*連絡先* という用語は URL キーとして使用できませんが、*連絡先* という用語を、別の文字または数字と組み合わせて使用することができます（例：*連絡先 1* および *連絡先 2*）。 用語は *contact+\&lt; 別の数字または文字\>* である必要はありませんが、長さが 255 文字を超えない限り、任意の文字列を指定できます。

次の手順を実行します。

1. Commerce管理者にログインします。
1. **[!UICONTROL Marketing]**/**[!UICONTROL SEO & Search]**/**[!UICONTROL URL Rewrites]** に移動します。
1. 「**[!UICONTROL Add URL Rewrite]**」をクリックします。
1. [!UICONTROL Create URL Rewrite] ドロップダウンで「*[!UICONTROL Custom]*」を選択します。
   1. [!UICONTROL Request Path] に「contact」と入力します。 ユーザーがブラウザーに入力するのは [!UICONTROL Request Path] であり、リダイレクト先は [!UICONTROL Target Path] であることに注意してください。
   1. [!UICONTROL Target Path] に、新しい URL キーを入力します（例：「contact1」）。
   1. [!UICONTROL Redirect] ドロップダウンで「*[!UICONTROL No]*」を選択します。

## 関連資料

* ユーザーガイドの [URL の書き換え ](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite)。
* ユーザーガイドの [SEO のベストプラクティス ](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/seo/seo-overview)。
