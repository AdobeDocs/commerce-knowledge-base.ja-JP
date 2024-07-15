---
title: EU のお客様は支払いを完了できません
description: この記事では、欧州連合（EU）のお客様が支払いを完了できない問題を修正しました。
exl-id: 8309d96b-47a3-4d27-b538-e6e3bcdfb7d4
feature: Orders, Payments
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# EU のお客様は支払いを完了できません

この記事では、欧州連合（EU）のお客様が支払いを完了できない問題を修正しました。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン
* Adobe Commerce オンプレミス 2.2.x、2.3.x
* Magento Open Source2.2.x, 2.3.x

## 問題

EU からのお客様は、クレジットカードの取引が拒否されていると不満を言っています。

## 原因：

欧州連合（EU）は、支払いサービスディレクティブ （PSD）と呼ばれる規制を、更新されたバージョン [PSD2](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32015L2366&amp;from=EN) で改訂しました。 これは、EU および欧州経済地域（EEA）全体で支払いサービスおよび支払いサービスプロバイダーを規制するために適用される欧州連合（EU）指令です。 強力な顧客認証（SCA）は、支払いデータのセキュリティと認証を向上させるためにPSD2 の要件です。 お客様の支払いソリューションがディレクティブの要件に準拠していない場合、お客様が支払いを完了できない可能性があります。 詳しくは、[ 関連のAdobe Commerce DevBlog 投稿 ](https://community.magento.com/t5/Magento-DevBlog/3D-Secure-2-0-changes/ba-p/136460) を参照してください。

## 解決策

DevBlog の [Adobe Commerce支払いプロバイダーのRecommendationsの節の推奨事項に従 ](https://community.magento.com/t5/Magento-DevBlog/3D-Secure-2-0-changes/ba-p/136460#recommendations) ます。
