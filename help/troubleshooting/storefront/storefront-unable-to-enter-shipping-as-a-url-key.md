---
title: URL キーとして配送を保存できない
description: ここでは、商品またはCMSページの URL キー（/shipping_など）として shipping を保存できない場合の問題の回避策を示します。 URL キーを保存しようとすると、URL キーが URL と重複していることを示すエラーが表示されます。
exl-id: df19b597-f615-4b19-82c1-59cc179fa720
feature: Marketing Tools, Shipping/Delivery, Storefront
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# _出荷_ を URL キーとして保存できません

ここでは、商品またはCMSページの URL キー（_例：/shipping_）として shipping を保存できない場合の問題の回避策を示します。 URL キーを保存しようとすると、URL キーが重複した URL であることを示すエラーが表示されます。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.x

## 問題

URL キーに _shipping_ という用語を使用してCMS ページを保存することはできません。

<u> 再現手順 </u>:

URL キーが _shipping_ の **[!UICONTROL CMS page]** を作成します。

<u> 期待される結果 </u>:

ページが、URL キーとして _shipping_ を使用して保存されます。

<u> 実際の結果 </u>:

このエラーが発生したため、保存できません：
*「URL キー」フィールドに指定された値は、既に存在する URL を生成します。*

## 原因：

送料は `vendor/magento/module-shipping/etc/frontend/routes.xml` で定義された予約語です。

```xml
<router id="standard">
      <route id="shipping" frontName="shipping">
          <module name="Magento_Shipping" />
      </route>
  </router>
```

## 解決策

URL キーに「_shipping_」という用語は使用できませんが、「_shipping_」という用語を、別の文字または数字（_例：shipping1 および shipping2_）と組み合わせて使用することはできます。

この用語は _shipping_+&lt; 別の数字または文字 > である必要はありませんが、長さが *255* 文字を超えない限り、任意の文字列を指定できます。

## 次の手順を実行します。

1. Adobe Commerce Admin にログインします。
1. **[!UICONTROL Marketing]**/**[!UICONTROL SEO & Search]**/**[!UICONTROL URL Rewrites]** に移動します。
1. 「**[!UICONTROL Add URL Rewrite]**」をクリックします。
1. **[!UICONTROL Create URL Rewrite]** ドロップダウンで「**[!UICONTROL Custom]**」を選択します。
   1. [!UICONTROL Request Path] を **_shipping_** と入力します。
   1. **[!UICONTROL Target Path]** に新しい URL キーを入力します（_例：&quot;shipping1&quot;_）。
   1. **[!UICONTROL Redirect]** ドロップダウンで「**[!UICONTROL No]**」を選択します。


      （**メモ**：リクエストパスは、ユーザーがブラウザーに入力するパスで、ターゲットパスは、リダイレクト先です。）

また、「*reserved*」というラベルの付いたこれらのキーワードを使用しても、同じ例外が表示されることはありません。 以下に示すこれらのキーワードのいずれかを URL キー値として使用すると、同じエラーが表示されます。


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

* アドビのマーチャンダイジングおよびプロモーションユーザーガイドの [URL の書き換え ](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite)。
* [SEO のベストプラクティス ](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/seo/seo-overview) マーチャンダイジングおよびプロモーションユーザーガイドの
