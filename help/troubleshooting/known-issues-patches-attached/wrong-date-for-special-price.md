---
title: 特別価格の日付が間違っています
description: この記事では、インターフェイスのロケールが異なる管理者がその値を変更した場合、「開始日」の商品の特別価格が正しくないという既知のAdobe Commerce 2.2.2 問題に対するパッチを提供します。
exl-id: fc109550-951e-4900-97e3-4ff3e7e5a395
feature: Orders, Personalization, User Account
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 特別価格の日付が間違っています

この記事では、インターフェイスのロケールが異なる管理者がその値を変更した場合、「開始日」の商品の特別価格が正しくないという既知のAdobe Commerce 2.2.2 問題に対するパッチを提供します。

## 問題

商品の特別価格を設定または変更すると、現在の日時が商品の値としてデータベースに保存されます。 `special_from_date` 属性（製品の編集時には表示されません）。 特別価格を編集し、管理者ユーザーアカウントが異なるインターフェイスロケールに設定されている場合、間違った値がに設定される可能性があります。 `special_from_date` 異なるロケールの日付形式の解析に問題があるため。

<u>再現手順</u>:

前提条件：管理者ユーザーのロケールが英語（米国）であること。

1. Commerce Admin にログインします。
1. 管理者ユーザーアカウント設定に移動します。
1. インターフェイスのロケールをウクライナ語に設定します。
1. クリック **アカウントを保存**.
1. に移動 **カタログ** > **製品**.
1. 任意の製品を選択します。
1. 製品ページで、 **詳細価格**.
1. 特別価格を追加してください。
1. 商品を保存します。
1. 手順 7～9 を繰り返します。
1. に移動 **システム** > **アクションログ**.
1. ログで製品のアップデートを確認します。

<u>期待される結果</u>:

特別価格の開始日は現在の日付にする必要があります。

<u>実際の結果</u>:

特別価格の開始日は数年後の日付であるため、特別価格が有効になりません。

## 解決策

パッチを適用すると、問題が再発するのを防ぐことができます。 日付が正しく設定されていない製品のデータを修正するには、パッチを適用した後で特別価格を再設定します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-11605\_EE\_2.2.2\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11605_EE_2.2.2_COMPOSER_v1.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* Adobe Commerce（すべてのデプロイメント方法） 2.2.2

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* Adobe Commerce オンプレミス 2.1.0 ～ 2.1.18、2.2.0 ～ 2.2.5
* クラウドインフラストラクチャー上のAdobe Commerce 2.1.11-2.1.18、2.2.0-2.2.5

## パッチの適用方法

参照： [Adobe Commerceが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 説明を参照してください。

## 添付ファイル