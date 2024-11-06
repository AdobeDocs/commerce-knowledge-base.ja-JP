---
title: 「MDVA-41628：制限付き管理者ユーザーが新しいリソースにアクセスする」
description: MDVA-41628 パッチは、新しいモジュールが追加されたときに、制限された管理者ユーザーが新しいリソースにアクセスできる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-41628。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 8f63ce9d-07b6-4d9d-a51b-b85b783b2adf
feature: Admin Workspace
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# MDVA-41628：制限付き管理者ユーザーは、新しいリソースにアクセスできます

MDVA-41628 パッチは、新しいモジュールが追加されたときに、制限された管理者ユーザーが新しいリソースにアクセスできる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.12 がインストールされている場合に使用できます。 パッチ ID は MDVA-41628。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

制限付き管理者ユーザーは、新しいモジュールが追加されると、新しいリソースにアクセスできます。

<u> 再現手順 </u>:

1. リソースが制限された管理者ユーザーロールを新規作成します。
1. 手順 1 で作成した役割の下に、新しい管理者ユーザーを作成します。
1. 新しいメニュー項目のセットと ACL リソースを作成するカスタムモジュールをインストールして有効にします。
1. 新しく作成した管理者ユーザーを使用してログインします。

<u> 期待される結果 </u>:

アクセスが制限された管理者ユーザーは、新しく作成されたメニュー項目にアクセスできません。

<u> 実際の結果 </u>:

制限付き管理者ユーザーは、新しいリソースがユーザーロールに割り当てられていない場合でも、新しいメニュー項目にアクセスできます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
