---
title: URL キーとして配送を保存できない
description: この記事では、製品または CMS ページの URL キー（/shipping_など）として shipping を保存できない場合の問題の回避策を説明します。 URL キーを保存しようとすると、URL キーが URL と重複していることを示すエラーが表示されます。
exl-id: df19b597-f615-4b19-82c1-59cc179fa720
feature: Marketing Tools, Shipping/Delivery, Storefront
role: Admin
source-git-commit: 1ce963142a261a17e2b42f79dd567c8484ec5b3e
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# 保存できません _送料_ URL キーとして

この記事では、URL キーとして送信を保存できない場合の問題の回避策を説明します（_例：/shipping_）に設定する必要があります。 URL キーを保存しようとすると、URL キーが重複した URL であることを示すエラーが表示されます。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.x

## 問題

CMS ページを次の用語で保存することはできません _送料_ を URL キーに入力します。

<u>再現手順</u>:

を作成 **[!UICONTROL CMS page]** URL キーがの場合 _送料_.

<u>期待される結果</u>:

ページがと共に保存されます _送料_ を URL キーとして使用します。

<u>実際の結果</u>:

このエラーが発生したため、保存できません：
*「URL キー」フィールドに指定した値は、既に存在する URL を生成します。*

## 原因：

送料は、で定義された予約語です。 `vendor/magento/module-shipping/etc/frontend/routes.xml`.

```xml
<router id="standard">
      <route id="shipping" frontName="shipping">
          <module name="Magento_Shipping" />
      </route>
  </router>
```

## 解決策

この用語は使用できません _送料_ URL キーに – という用語を使用できます _送料_ 他の文字または数字（_例：shipping1 および shipping2_）に設定します。

という用語は必須ではありませんが、 _送料_+&lt;another number=&quot;&quot; or=&quot;&quot; letter=&quot;&quot;>  – 長さが以下である限り、用語は任意の文字列にすることができます *255* 文字。

## 次の手順を実行します。

1. Adobe Commerce Admin にログインします。
1. に移動 **[!UICONTROL Marketing]** > **[!UICONTROL SEO & Search]** > **[!UICONTROL URL Rewrites]**.
1. クリック **[!UICONTROL Add URL Rewrite]**.
1. を選択 **[!UICONTROL Custom]** が含まれる **[!UICONTROL Create URL Rewrite]** ドロップダウン。
   1. を入力 [!UICONTROL Request Path] as **_送料_**.
   1. が含まれる **[!UICONTROL Target Path]**：新しい URL キー（_例：「shipping1」_）に設定します。
   1. を選択 **[!UICONTROL No]** が含まれる **[!UICONTROL Redirect]** ドロップダウン。


      （**注意**：リクエストパスは、ユーザーがブラウザーに入力するパスで、ターゲットパスは、リダイレクト先のパスです）。

また、というラベルが付いているこれらのキーワードの使用は避けてください *予約済み* 同じ例外が表示されるキーワード。 以下に示すこれらのキーワードのいずれかを URL キー値として使用すると、同じエラーが表示されます。


```
"admin"
"adminAnalytics"
"analytics"
"api"
"backup"
"bulk"
"captcha"
"catalog"
"catalogsearch"
"checkout"
"cms"
"contact"
"cookie"
"customer"
"directory"
"downloadable"
"giftmessage"
"groupedProduct"
"indexer"
"instantpurchase"
"loginascustomer"
"marketplace"
"mui"
"multishipping"
"newsletter"
"oauth"
"paypal"
"persistent"
"productalert"
"releaseNotification"
"reports"
"review"
"robots"
"rss"
"sales"
"search"
"security"
"sendfriend"
"shipping"
"stores"
"swagger"
"swatches"
"tax"
"theme"
"translation"
"vault"
"wishlist"
```

## 関連資料

* [URL リライト](https://docs.magento.com/user-guide/marketing/url-rewrite.html) 詳しくは、マーチャンダイジングおよびプロモーションユーザーガイドを参照してください。
* [SEO のベストプラクティス](https://docs.magento.com/user-guide/marketing/seo-best-practices.html) アドビのマーチャンダイジングおよびプロモーションユーザーガイドの
