---
title: 「MDVA-42269:「TypeError」エラーにより、管理者ユーザーが管理者にログインできない」
description: MDVA-42269 パッチを適用すると、TypeError が原因で管理者ユーザーが管理者にログインできない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.11 がインストールされている場合に利用できます。  パッチ ID は MDVA-42269。  最新のパッチアップデートは QPT 1.1.15 にあります。この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 66d744a2-054e-493c-a060-9ed78447e35b
feature: Admin Workspace
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# MDVA-42269:「TypeError」エラーにより、管理者ユーザーが管理者にログインできない

MDVA-42269 パッチを適用すると、TypeError が原因で管理者ユーザーが管理者にログインできない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.11 がインストールされている場合に使用できます。  パッチ ID は MDVA-42269。  最新のパッチアップデートは QPT 1.1.15 にあります。この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1、2.3.7-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1 - 2.4.3-p2、2.3.7-p3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

次のエラーのため、管理者ユーザーは管理者にログインできません：*TypeError: strtotime （）は、パラメーター 1 が文字列であること、null が指定されていることを想定しています。*

<u> 再現手順 </u>:

Commerce Admin にログインします。

<u> 期待される結果 </u>:

管理者ユーザーは、正しいユーザー名とパスワードでログインできます。

<u> 実際の結果 </u>:

管理者ユーザーはログインできません。 次のエラーがログに記録されます。*TypeError:strtotime （）は、パラメーター 1 が文字列であることが想定されます。null が指定されています。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
