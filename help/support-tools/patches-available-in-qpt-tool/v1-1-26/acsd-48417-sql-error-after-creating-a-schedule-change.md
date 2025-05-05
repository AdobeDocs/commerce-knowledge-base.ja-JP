---
title: 「ACSD-48417：スケジュール変更の作成後の SQL エラー」
description: ACSD-48417 パッチを適用すると、商品のスケジュールを変更して別の商品を保存した後に SQL エラーが表示されるAdobe Commerceの問題を修正できます。
exl-id: 2bbf3bb5-dec8-43b3-81f1-be0dc53d1f46
feature: Storage
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# ACSD-48417：スケジュール変更の作成後の SQL エラー

ACSD-48417 パッチは、製品のスケジュール変更を作成して別の製品を保存した後に SQL エラーが表示される問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされている場合に使用できます。 パッチ ID は ACSD-48417 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品のスケジュール変更を作成して別の製品を保存すると、SQL エラーが表示されます。

<u> 再現手順 </u>:

1. Magento 2.4 をインストールし、EE とサンプルデータを開発します。
1. 管理パネル/**[!UICONTROL Catalog]**/**[!UICONTROL Products]** に移動します。
1. 任意の製品を編集します（例：Joust Duffle Bag[SKU: 24-MB01]）。
1. 新しい更新をスケジュールする：
   * Select **[!UICONTROL Save as a New Update]**
   * 更新名：「Update 1」
   * 開始日：現在の時刻+1 分
   * 終了日：現在の時刻+1 時間
   * 製品名を「Joust Duffle Bag 2」に変更します。
   * 商品を保存します。
1. CLI に移動し、cron を実行して、スケジュールが適用されるまで待ちます。

   ```
   bin/magento cron:run && bin/magento cron:run
   ```

1. もう一度、**[!UICONTROL Catalog]**/**[!UICONTROL Products]** に移動して、設定可能な製品（例：Chaz Kangereo Hoodie[SKU:MH01]）を編集します。

   * すべてのバリアントを無効にします。 アクション列/ **[!UICONTROL Select]** / **[!UICONTROL Disable Product]** に移動します。
   * 設定可能なものを保存します。

<u> 期待される結果 </u>:

商品の保存時にエラーは発生しません。

<u> 実際の結果 </u>:

次のエラーが発生します。

```SQL
SQLSTATE[23000]: Integrity constraint violation: 1048 Column 'sku' cannot be null, query was: INSERT INTO `catalog_product_entity` (`entity_id`, `sku`, `row_id`, `created_in`, `updated_in`) VALUES (?, ?, ?, ?, ?)
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
