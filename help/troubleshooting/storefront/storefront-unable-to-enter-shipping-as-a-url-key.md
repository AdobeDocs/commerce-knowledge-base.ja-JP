---
title: 「送料」を URL キーとして保存できません
description: この記事では、「shipping」を製品または CMS ページの URL キー（「/shipping」など）として保存できない場合の問題の回避策を説明します。 URL キーを保存しようとすると、URL キーが重複した URL であることを示すエラーが表示されます。
exl-id: df19b597-f615-4b19-82c1-59cc179fa720
feature: Marketing Tools, Shipping/Delivery, Storefront
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# 「送料」を URL キーとして保存できません

この記事では、「shipping」を製品または CMS ページの URL キー（「/shipping」など）として保存できない場合の問題の回避策を説明します。 URL キーを保存しようとすると、URL キーが重複した URL であることを示すエラーが表示されます。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.x

## 問題

URL キーに「shipping」という語句を含む CMS ページを保存することはできません。

<u>再現手順</u>:

URL キーが「shipping」の CMS ページを作成します。

<u>期待される結果</u>:

ページが URL キーに「shipping」とともに保存されます。

<u>実際の結果</u>:

保存できず、次のエラーが表示されます。 *「URL キー」フィールドに指定した値は、既に存在する URL を生成します。*

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

URL キーに「shipping」という用語は使用できませんが、「shipping」という用語を別の文字または数字と組み合わせて使用することはできます（「shipping1」や「shipping2」など）。 「送料」という用語は必須ではありませんが、&lt;another number=&quot;&quot; or=&quot;&quot; letter=&quot;&quot;>  – 長さが 255 文字を超えない限り、用語は任意の文字列にすることができます。

次の手順を実行します。

1. Commerce Admin にログインします。
1. に移動 **Marketing** > SEO と検索 > **URL リライト**.
1. クリック **URL 書き換えの追加**.
1. を選択 *カスタム* URL 書き換えを作成ドロップダウンで、
   1. リクエストパス「shipping」を入力します。 メモ：リクエストパスは、ユーザーがブラウザーに入力するパスで、ターゲットパスは、リダイレクト先のパスです。
   1. 「ターゲットパス」に新しい URL キーを入力します（例：「shipping1」）。
   1. を選択 **不可** 「リダイレクト」ドロップダウンで、次の操作を行います。

## 関連資料

* [URL リライト](https://docs.magento.com/user-guide/marketing/url-rewrite.html) を参照してください。
* [SEO のベストプラクティス](https://docs.magento.com/user-guide/marketing/seo-best-practices.html) を参照してください。
