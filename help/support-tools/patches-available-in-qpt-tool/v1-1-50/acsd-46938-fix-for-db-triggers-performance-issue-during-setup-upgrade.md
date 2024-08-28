---
title: 「ACSD-46938:「setup:upgrade」中に DB トリガーでパフォーマンスの問題が発生する
description: ACSD-46938 パッチを適用して、「setup:upgrade」コマンドがインデクサーモードをスケジュールから保存に変更し、パフォーマンスの著しい低下を引き起こすAdobe Commerceの問題を修正してください。
feature: Upgrade
role: Admin, Developer
source-git-commit: cbd16ac7c6d6d7a4e3786880409475a10964c070
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# ACSD-46938:`setup:upgrade` ークフロー中に DB トリガーでパフォーマンスの問題が発生する

ACSD-46938 パッチでは、`setup:upgrade` コマンドがインデクサーモードをスケジュールから保存に変更し、パフォーマンスの大幅な低下を引き起こす問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.50 がインストールされている場合に使用できます。 パッチ ID は ACSD-46938 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p9

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`setup:upgrade` で DB トリガーを再作成する際にパフォーマンスが低下します。

<u> 再現手順 </u>:

1. 多くの製品やカテゴリを含む大規模なカタログを作成します。
1. [!UICONTROL Admin] にログインします。
1. すべてのインデクサーを [!UICONTROL Update By Schedule] モードに設定します。
1. 任意の製品を開きます。
1. 更新します。 例えば、新しいカテゴリを割り当てます。
1. 「[!UICONTROL Save]」をクリックします。
1. `bin/magento setup:upgrade` コマンドと `bin/magento cron:run` コマンドを並行して実行します。

<u> 期待される結果 </u>:

`bin/magento cron:run` のコマンドを同時に実行すると、`bin/magento setup:upgrade` のコマンドの実行時間が大幅に長くなる。

<u> 実際の結果 </u>:

コマンドの実行時間は増えません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
