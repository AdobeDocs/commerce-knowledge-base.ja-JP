---
title: '*contact*をURL キーとして保存できません'
description: この記事では、製品またはCMS ページのURL キー（「/contact」など）として*contact*を保存できない場合の問題の回避策を説明します。 URL キーを保存しようとすると、URL キーが重複するURLであることを示すエラーが表示されます。
exl-id: eb340813-aba5-43a4-af5d-8fb64c93e021
feature: CMS, Marketing Tools, Storefront
role: Admin
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%
---
# *連絡先*&#x200B;をURL キーとして保存できません

この記事では、製品またはCMS ページのURL キー（「/contact」など）として&#x200B;*contact*&#x200B;を保存できない場合の問題に対する回避策を説明します。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.x

## イシュー

*contact*&#x200B;という用語をURL キーとして使用して、商品またはCMS ページを保存することはできません。 URL キーを保存しようとすると、URL キーが重複するURLであることを示すエラーが表示されます。

<u>複製する手順</u>:

*contact*&#x200B;をURL キーとするCMS ページを作成します。

<u>期待される結果</u>:

ページは&#x200B;*contact*&#x200B;とともにURL キーとして保存されます。

<u>実際の結果</u>:

ページを保存できません。 次のエラーが発生します。*URL キーのフィールドで指定された値は、既に存在するURLを生成します。*

## 原因

*連絡先*&#x200B;は、`vendor/magento/module-contact/view/frontend/layout/contact_index_index.xml`で定義された予約語です。

```xml
<router id="standard">
      <route id="contact" frontName="contact">
          <module name="Magento_Contact" />
      </route>
  </router>
```

## Solution

*contact*&#x200B;という用語をURL キーとして使用することはできませんが、*contact*&#x200B;という用語を別の文字または数字と組み合わせて使用することはできます（例：*contact1*&#x200B;と&#x200B;*contact2*）。 用語は&#x200B;*contact+\&lt;別の数字または文字\>*&#x200B;である必要はありませんが、長さが255文字を超えない限り、用語は任意の文字列にすることができます。

次の手順を実行します。

1. Commerce Adminにログインします。
1. **[!UICONTROL Marketing]** > **[!UICONTROL SEO & Search]** > **[!UICONTROL URL Rewrites]**&#x200B;に移動します。
1. **[!UICONTROL Add URL Rewrite]**&#x200B;をクリックします。
1. [!UICONTROL Create URL Rewrite] ドロップダウンで「*[!UICONTROL Custom]*」を選択します。
   1. [!UICONTROL Request Path]に「連絡先」と入力します。 [!UICONTROL Request Path]はユーザーがブラウザーに入力したもので、[!UICONTROL Target Path]はリダイレクト先であることに注意してください。
   1. [!UICONTROL Target Path]に、新しいURL キー（「contact1」など）を入力します。
   1. 「[!UICONTROL Redirect]」ドロップダウンで「*[!UICONTROL No]*」を選択します。

## 関連トピックス

* ユーザーガイドの[URL書き換え](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite)。
* ユーザーガイドの[SEOのベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/seo-overview)。
