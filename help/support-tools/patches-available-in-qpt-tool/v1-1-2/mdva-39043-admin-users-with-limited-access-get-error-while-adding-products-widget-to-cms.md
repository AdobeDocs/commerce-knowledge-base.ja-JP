---
title: 「MDVA-39043：管理者ユーザーがCMS ページにウィジェットを追加する際にエラーが発生する」
description: MDVA-39043 パッチでは、アクセス権が制限された管理者ユーザーが「Products」ウィジェットをCMS ページに追加する際にエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/patches/overview） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-39043。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 63057351-e972-4575-9bf0-e818f590b40a
feature: Admin Workspace, CMS, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# MDVA-39043：管理者ユーザーがCMS ページにウィジェットを追加するとエラーが発生する

MDVA-39043 パッチでは、アクセス権が制限された管理者ユーザーが「Products」ウィジェットをCMS ページに追加する際にエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/patches/overview)1.1.2 がインストールされている場合に使用できます。 パッチ ID は MDVA-39043。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.4 - 2.4.3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

限定アクセスを持つ管理者ユーザーが、「Products」ウィジェットをCMS ページに追加するとエラーが発生する。

<u> 再現手順 </u>:

1. 管理者とアクセス権のみを使用してバックエンドにログインし、コンテンツを編集します。
1. **コンテンツ**/**ページ** に移動します。
1. 編集するページを開きます。
1. **ページビルダー** でコンテンツを編集します。
1. **コンテンツを追加** セクションから **製品** ウィジェットを追加します。
1. **製品** ウィジェットの **設定** をクリックします。

<u> 期待される結果 </u>:

エラーは表示されません。

<u> 実際の結果 </u>:

次のエラーメッセージが表示されます。

`*A technical problem with the server created an error. Try again to continue what you were doing. If the problem persists, try again later.*`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
