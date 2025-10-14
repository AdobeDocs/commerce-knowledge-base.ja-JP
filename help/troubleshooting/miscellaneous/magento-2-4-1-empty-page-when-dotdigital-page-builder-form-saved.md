---
title: 「Adobe Commerce 2.4.1:dotdigital ページビルダーフォームを保存した場合のページが空になる」
description: この記事では、Safari ブラウザーを使用する際に、管理パネルで dotdigital ページビルダーフォームを保存した後に空の web ページが表示される、Adobe Commerce 2.4.1 の既知の問題の回避策を説明します。
exl-id: 682eac73-1ad2-4093-acfb-6a8da4c05cf5
feature: Page Builder
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Adobe Commerce 2.4.1:dotdigital ページビルダーフォームを保存した際に、ページが空になる

この記事では、Safari ブラウザーを使用する際に、管理パネルで dotdigital ページビルダーフォームを保存した後に空の web ページが表示される、Adobe Commerce 2.4.1 の既知の問題の回避策を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.1
* クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

## 問題

<u> 再現手順 </u>

1. **管理パネル**/**コンテンツ**/**ページ** に移動し、任意のページの **編集** を選択します。
1. **コンテンツ** に移動し、「**ページビルダーで編集** ボタンをクリックします。
1. **dotdigital フォーム** ブロックをドラッグして、「**編集**」を選択します。
1. テストフォームの 1 つを選択してから、**埋め込み** モードを選択してフォームを保存します。
1. ページ変更を保存します。

<u> 期待される結果：</u>

Web ページは正常に保存されます。

<u> 実際の結果：</u>

Web ページは空です。 Web ページを再読み込みすると、変更が適用されます。

## 回避策

回避策は、Safari の別のブラウザーを使用することです。 この問題は、2021 年第 1 四半期の次回リリースのAdobe Commerce 2.4.2 で修正される予定です。

## 関連資料

* [&#x200B; ページビルダーとは？開発者向けドキュメントを &#x200B;](https://developer.adobe.com/commerce/frontend-core/page-builder/) 照してください。
* 開発者向けドキュメントの [&#x200B; ページビルダーの設定 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/setup.html?lang=ja)。
* ユーザーガイドの [&#x200B; ページビルダー &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/page-builder/introduction)。
* ユーザーガイドの [&#x200B; ページビルダー – 要素 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/page-builder/workspace#elements)。
