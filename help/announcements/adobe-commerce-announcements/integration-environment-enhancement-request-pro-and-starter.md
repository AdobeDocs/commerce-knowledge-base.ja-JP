---
title: 統合環境の強化リクエスト - Pro と Starter
description: Adobe Commerce on cloud infrastructure Pro プランアーキテクチャのお客様が標準サイズの統合環境を使用している場合、またはAdobe Commerce on cloud infrastructure Starter プランアーキテクチャのお客様が標準サイズのステージング環境を使用しており、より多くの電力を必要としている場合は、Enhanced Integration Environments へのアップグレードをリクエストできます。このアップグレードにより、およそ 4 倍のパフォーマンスが得られます。 この記事では、Pro のお客様と Starter のお客様の説明を分けています。
exl-id: c49b049b-efb8-412f-b27d-a89f8a758d85
feature: Integration
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---

# 統合環境の強化リクエスト - Pro と Starter

Adobe Commerce on cloud infrastructure Pro プランアーキテクチャのお客様が標準サイズの統合環境を使用している場合、またはAdobe Commerce on cloud infrastructure Starter プランアーキテクチャのお客様が標準サイズのステージング環境を使用しており、より多くの電力を必要としている場合は、Enhanced Integration Environments へのアップグレードをリクエストできます。このアップグレードにより、およそ 4 倍のパフォーマンスが得られます。 この記事では、Pro のお客様と Starter のお客様の説明を分けています。

>[!NOTE]
>
> 拡張統合にアップグレードすると、サードパーティの統合やカスタマイズを含むインストールの総リソース要件に応じてパフォーマンス上の問題がすべて解決されるわけではありません。
>
> また、統合環境でのベストパフォーマンスを得るために、ベストプラクティスに従っていることを確認する必要があります。さらに、それがエンドオールのソリューションではない場合もあります。 Commerce on Cloud Infrastructure ガイドのガイダンス「[Pro アーキテクチャ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/architecture/pro-architecture#integration-environment) および [ スターターアーキテクチャ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/architecture/starter-architecture#staging-environment)」については、次のドキュメントを参照してください。

## プロ

1. Pro を使用している場合をアップグレードするには、統合ブランチの数を 2 つに減らす必要があります（**メインの統合ブランチが合計に含まれます**）。 **注意：この合計でプライマリ・ブランチはカウントしないでください。 プライマリブランチは統合ブランチとは見なされません。** 開発者向けドキュメントの [Cloud Console を使用したブランチの管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/console-branches.html) の手順に従います。
1. マーチャントは、問い合わせ理由 [ クラウド設定の変更をリクエスト ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)」を使用して、拡張統合環境へのアップグレードをリクエスト *サポートチケットを送信* する必要があります。
1. Adobeカスタマー・エンジニアリング・チームが統合環境の数を確認し、変更を開始します。
1. アップグレードが完了すると、マーチャントにチケットで通知されます。
1. マーチャントは統合環境をデプロイします。 開発者向けドキュメントの [ ブランチの結合 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches#merge-a-branch) の手順に従います。 *注意*：デプロイメントは次の場合に自動的に行われます。 <pre>git プッシュオリジン &lt;branch-name></pre>

パフォーマンスが向上した場合は、拡張統合環境に正常にアップグレードされたことを示します。

**注**:

* 標準サイズと拡張サイズの 2 種類しか使用できません。
* 特定のストアのすべての統合環境のサイズは同じなので、個別にサイズ変更することはできません。
* 2 つ以上の Enhanced Integration 環境が必要な場合は、Adobeアカウントチームにお問い合わせください。

## スターター

1. スタータープランには統合分岐を含めることはできません。マーチャントは統合環境を削除し、ステージング環境のみから移動する必要があります。 開発者向けドキュメントの [Cloud Console を使用したブランチの管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/console-branches.html) の手順に従います。 利用可能な環境の数が減り、最大 1 つの統合環境が可能になります。
1. マーチャントは、問い合わせ理由 [ 「クラウド設定の変更をリクエスト ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)」 *-**ステージング環境は名前付き統合環境です* を使用して、拡張統合環境へのアップグレードをリクエストするサポートチケットを送信** する必要があります。
1. Adobeカスタマー・エンジニアリング・チームが統合環境の数を確認し、変更を開始します。
1. アップグレードが完了すると、マーチャントにチケットで通知されます。
1. マーチャントは統合環境をデプロイします。 開発者向けドキュメントの [ ブランチの結合 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches#merge-a-branch) の手順に従います。 *注意*：デプロイメントは次の場合に自動的に行われます。 <pre>git プッシュオリジン &lt;branch-name></pre>

パフォーマンスが向上した場合は、拡張統合環境に正常にアップグレードされたことを示します。

**注**:

* 標準サイズと拡張サイズの 2 種類しか使用できません。
* 特定のストアのすべての統合環境のサイズは同じなので、個別にサイズ変更することはできません。
* ステージングを超える統合環境が必要な場合は、Adobeアカウントチームにお問い合わせください。
* 2020 年 9 月 17 日以降に購入された場合、統合環境が拡張されているので、この機能強化は適用されません。
