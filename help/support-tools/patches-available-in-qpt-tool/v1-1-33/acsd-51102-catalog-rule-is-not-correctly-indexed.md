---
title: 「ACSD-51102：多数の製品に適用されたカタログルールのインデックスが正しくない」
description: ACSD-51102 パッチを適用すると、Adobe Commerceの問題を修正できます。この問題では、スケジュールされた更新によってルールが有効になると、多数の商品に適用されるカタログルールのインデックスが正しく作成されません。
feature: Catalog Management, Products
role: Admin
exl-id: 5c1c5f9c-9cce-4b11-8058-0e12a4bf93fd
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# ACSD-51102：多数の製品に適用されているカタログルールが正しくインデックス化されていない

ACSD-51102 パッチを適用すると、スケジュールされた更新によってルールが有効にされたときに、多数の製品に適用されるカタログルールが正しくインデックス化されない問題が修正されます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-51102 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

スケジュールされた更新でルールが有効になっている場合、多数の製品に適用されているカタログルールのインデックスが正しく作成されません。

前提条件：

* Cron ジョブは毎分設定され実行されます。

<u> 再現手順 </u>:

1. カタログルールが有効な場合の *カタログルール* インデクサーの実行時間を 120 秒以上に短縮するために、何千もの製品で大きなカタログを作成します。
2. *アクティブ* ステータスが *いいえ* に設定された 2 つのカタログルールを作成します。  例えば、*Test 1* や *Test 2* などです。 各ルールはカタログ内のすべての製品に影響し、インデクサーが 120 秒以上実行される必要があります。
3. インデクサーのステータスが *準備完了* であることを確認します。
4. スケジュールされた更新を作成して、これら 2 つのルールを有効にします。 *テスト 2* スケジュールは *テスト 1* の直後に開始します。 例えば、1 分の差があるとします。
5. ストアフロントにて商品価格をご確認ください。

<u> 期待される結果 </u>

両方のルールの割引が適用されます。

<u> 実績 </u>

最初のルールの割引のみが適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>)」を参照してください。
