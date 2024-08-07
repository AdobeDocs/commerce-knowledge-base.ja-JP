---
title: 「MDVA-29959 パッチ：「顧客」権限を持つ管理者が会社アカウントを管理できない」
description: '[ 品質向上パッチツール（QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md）ツールバージョン 1.0.5 で利用可能な MDVA-29959 パッチにより、「顧客」 ACL のすべての権限を持つ制限付き管理者ユーザーが会社を管理（会社を追加または削除）できない問題が修正されました。 この問題は、Adobe Commerce 2.3.4 の B2B で修正されていることに注意してください。'
exl-id: ee246380-d37e-4c24-8435-97ae80088227
feature: Admin Workspace, B2B, Companies, Roles/Permissions
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# MDVA-29959 パッチ：「顧客」権限を持つ管理者が会社アカウントを管理できない

[ 品質向上パッチツール（QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) ツールバージョン 1.0.5 で利用できる MDVA-29959 パッチにより、「顧客」 ACL のすべての権限を持つ制限付き管理者ユーザーが会社を管理（会社を追加または削除）できない問題が修正されました。 この問題は、Adobe Commerce 2.3.4 の B2B で修正されていることに注意してください。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerceの B2B 2.3.0-2.3.3-p1。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「顧客」 ACL に対するすべての権限を持つ管理者ユーザーが、会社を管理（会社を追加または削除）することはできません。

<u> 再現手順 </u>

1. Commerce管理者で、新しい管理者ロールを作成し、そのロールにユーザーを割り当てます。
1. 「顧客」リソースのみを役割に割り当てます。
1. この役割を持つユーザーとしてログインします。
1. 会社アカウントを削除してみてください。

<u> 期待される結果：</u>

会社アカウントが正常に削除されました。

<u> 実際の結果：</u>

会社アカウントを削除することはできません。 *申し訳ありませんが、このコンテンツを表示するには権限が必要です。エラ* メッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
