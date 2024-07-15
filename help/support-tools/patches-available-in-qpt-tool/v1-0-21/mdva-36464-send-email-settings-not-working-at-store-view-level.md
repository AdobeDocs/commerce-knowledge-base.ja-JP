---
title: 「MDVA-36464：送信メールの設定がストア表示レベルで機能しない」
description: MDVA-36464 パッチでは、送信メールの設定がストアビューレベルで機能しない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.21 がインストールされている場合に利用できます。 パッチ ID は MDVA-36464。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: cdf7e208-90ee-4711-8407-026da42fe3c8
feature: Communications
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# MDVA-36464：送信メールの設定がストア表示レベルで機能しない

MDVA-36464 パッチでは、送信メールの設定がストアビューレベルで機能しない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.21 がインストールされている場合に使用できます。 パッチ ID は MDVA-36464。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.4.0-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 前提条件：</u>

クリーンなAdobe Commerceをインストールします。

<u> 再現手順 </u>:

1. 追加の web サイト、ストア、ストア表示を作成します（この例では、2 つ目の web サイトは *website2*）です。
1. **ストア**/**設定**/**詳細**/**システム**/**メール送信設定** で、グローバルレベルの **メール通知** を無効にします。
1. *website2* レベルで **メール通知** を有効にします（**メール通信を無効にする** = *No*）。
1. Admin で新しいユーザーを作成し、そのユーザーを *website2* に割り当てます。
1. Admin で、顧客の編集ページの、上記の手順 4 で作成した顧客の **パスワードをリセット** をクリックします。

<u> 期待される結果 </u>:

2 つ目の web サイトの場合は **メール通信を無効にする** = *いいえ* なので（例：*website2*）、**ようこそメール** と **パスワードリセットメール** の両方が期待どおりに送信されます。

<u> 実際の結果 </u>:

* 新しい顧客の作成後の **ようこそメール** はトリガーされません。
* **パスワードリセットメール** がトリガーされない。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
