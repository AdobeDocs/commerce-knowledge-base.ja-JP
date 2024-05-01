---
title: 「B2B：会社がストアフロントのプロファイルページにアクセスできない」
description: この記事では、ストアフロントで登録会社のアカウントページでエラーが発生する問題に関連する、Adobe Commerce 2.2.4 B2B の既知の問題に対するパッチを提供します。
exl-id: 5f0d81a2-e0a1-487b-8a4f-28b8cb704e32
feature: B2B, Companies
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# B2B：企業がストアフロントのプロファイルページにアクセスできない

この記事では、ストアフロントで登録会社のアカウントページでエラーが発生する問題に関連する、Adobe Commerce 2.2.4 B2B の既知の問題に対するパッチを提供します。

## 問題

顧客（会社）は、サイト上に会社アカウントを正常に作成できますが、 *「customerId =」を持つそのようなエンティティはありません* および *「まだ会社アカウントがありません」* エラーメッセージ。 また、以下の情報も得られます。 *&quot;500 内部サーバーエラー&quot;* 会社プロファイルページにアクセスしようとしたとき。

## パッチ

パッチが適用されたアーカイブをダウンロードするには、次のリンクをクリックします。

[MDVA-9013\_EE\_2.2.2\_composer.patch のダウンロード](assets/MDVA-9013_EE_2.2.2_composer.patch.zip)

### 互換性のあるAdobe Commerce バージョン

パッチは次のために作成されました。

* Adobe Commerce オンプレミス 2.2.2

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* クラウドインフラストラクチャー上のAdobe Commerce（2.2.0 から 2.2.4 へ）
* Adobe Commerce オンプレミス（2.2.0 から 2.2.1 および 2.2.3 から 2.2.4）

## パッチの適用方法

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 説明を参照してください。
