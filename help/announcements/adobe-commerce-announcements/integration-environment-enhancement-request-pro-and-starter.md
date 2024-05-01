---
title: 統合環境の強化リクエスト - Pro と Starter
description: Adobe Commerce on cloud infrastructure Pro プランアーキテクチャのお客様が標準サイズの統合環境を使用している場合、またはAdobe Commerce on cloud infrastructure Starter プランアーキテクチャのお客様が標準サイズのステージング環境を使用しており、より多くの電力を必要としている場合は、Enhanced Integration Environments へのアップグレードをリクエストできます。このアップグレードにより、およそ 4 倍のパフォーマンスが得られます。 この記事では、Pro のお客様と Starter のお客様の説明を分けています。
exl-id: c49b049b-efb8-412f-b27d-a89f8a758d85
feature: Integration
role: Admin
source-git-commit: 43be85de953909253900d60488f76a20bac91793
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# 統合環境の強化リクエスト - Pro と Starter

Adobe Commerce on cloud infrastructure Pro プランアーキテクチャのお客様が標準サイズの統合環境を使用している場合、またはAdobe Commerce on cloud infrastructure Starter プランアーキテクチャのお客様が標準サイズのステージング環境を使用しており、より多くの電力を必要としている場合は、Enhanced Integration Environments へのアップグレードをリクエストできます。このアップグレードにより、およそ 4 倍のパフォーマンスが得られます。 この記事では、Pro のお客様と Starter のお客様の説明を分けています。

## プロ

1. Pro を使用している場合をアップグレードするには、統合ブランチの数を 2 に減らす必要があります（**main Integration ブランチが合計に含まれます**）に設定します。 **注意：この合計にプライマリ・ブランチはカウントしないでください。 プライマリブランチは統合ブランチとは見なされません。** の手順に従います [Cloud Console を使用したブランチの管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/console-branches.html) 開発者向けドキュメントを参照してください。
1. 商人は必要があります [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) 連絡先理由「」を使用して、拡張統合環境へのアップグレードをリクエストする&#x200B;*クラウド設定変更のリクエスト*」と入力します。
1. Adobeカスタマー・エンジニアリング・チームが統合環境の数を確認し、変更を開始します。
1. アップグレードが完了すると、マーチャントにチケットで通知されます。
1. マーチャントは統合環境をデプロイします。 の手順に従います [ブランチの結合](https://devdocs.magento.com/cloud/env/environments-start.html#merge) 開発者向けドキュメントを参照してください。 *注意*：デプロイメントは次を実行すると自動的に行われます。 <pre>git プッシュオリジン <branch-name></pre>

パフォーマンスが向上した場合は、拡張統合環境に正常にアップグレードされたことを示します。

**備考**:

* 標準サイズと拡張サイズの 2 種類しか使用できません。
* 特定のストアのすべての統合環境のサイズは同じなので、個別にサイズ変更することはできません。
* 2 つ以上の Enhanced Integration 環境が必要な場合は、Adobeアカウントチームにお問い合わせください。

## スターター

1. スタータープランには統合分岐を含めることはできません。マーチャントは統合環境を削除し、ステージング環境のみから移動する必要があります。 の手順に従います [Cloud Console を使用したブランチの管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/console-branches.html) 開発者向けドキュメントを参照してください。 利用可能な環境の数が減り、最大 1 つの統合環境が可能になります。
1. 商人は必要があります [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) 連絡先理由を使用して、拡張統合環境へのアップグレードをリクエストする *「クラウド設定の変更をリクエスト」* -  **ステージング環境は名前付き統合環境です**.
1. Adobeカスタマー・エンジニアリング・チームが統合環境の数を確認し、変更を開始します。
1. アップグレードが完了すると、マーチャントにチケットで通知されます。
1. マーチャントは統合環境をデプロイします。 の手順に従います [ブランチの結合](https://devdocs.magento.com/cloud/env/environments-start.html#merge) 開発者向けドキュメントを参照してください。 *注意*：デプロイメントは次を実行すると自動的に行われます。 <pre>git プッシュオリジン <branch-name></pre>

パフォーマンスが向上した場合は、拡張統合環境に正常にアップグレードされたことを示します。

**備考**:

* 標準サイズと拡張サイズの 2 種類しか使用できません。
* 特定のストアのすべての統合環境のサイズは同じなので、個別にサイズ変更することはできません。
* ステージングを超える統合環境が必要な場合は、Adobeアカウントチームにお問い合わせください。
* 2020 年 9 月 17 日以降に購入された場合、統合環境が拡張されているので、この機能強化は適用されません。
