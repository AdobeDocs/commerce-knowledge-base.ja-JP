---
title: 「ACSD-57086：利用条件が有効なデフォルト以外の web サイトからの注文が正しく処理されない」
description: ACSD-57086 パッチを適用すると、利用条件が有効なデフォルト以外の web サイトから注文が正しく処理されないAdobe Commerceの問題を修正できます。
feature: Orders
role: Admin, Developer
source-git-commit: ab90568b0333415e73ca42b9c127a2a599f00aa7
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# ACSD-57086：利用条件が有効なデフォルト以外の web サイトからの注文が正しく処理されない

ACSD-57086 パッチは、契約条件が有効になっているデフォルト以外の web サイトから注文した注文が正しく処理されない問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.49 がインストールされている場合に使用できます。 パッチ ID は ACSD-57086 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p7

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

AsyncOrder 処理でマルチストア設定を使用する際に、キューの消費者コードの範囲処理に関する問題が原因で、メインの web サイト以外の web サイト/ストアで注文が拒否されます。

<u> 再現手順 </u>:

1. [!DNL RabbitMQ] をインストールして `bin/magento setup:upgrade` を実行し、[!DNL RabbitMQ] 用のキューを作成します。
1. 次を使用して AsyncOrder 処理を設定します。

   ```bash
   bin/magento setup:config:set --checkout-async 1
   ```

1. セカンダリ Web サイト、ストア、ストアビューを作成します。
1. 両方の web サイト間で共有される製品を作成します。
1. 利用条件を有効にする：
   1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Sales]**/**[!UICONTROL Checkout]**/**[!UICONTROL Checkout Options]** に移動します。
   1. *[!UICONTROL Enable Terms And Conditions]* を *はい* に設定します。
1. 両方の web サイトの利用条件を設定します。
   1. **[!UICONTROL Stores]**/**[!UICONTROL Terms And Conditions]**/**[!UICONTROL Add New Condition]** に移動します。
   1. 次の設定を使用します。
      * *[!UICONTROL Condition Name]*: *すべて*
      * *[!UICONTROL Status]*: *[!UICONTROL Enabled]*
      * *[!UICONTROL Applied]*: *[!UICONTROL Manually]*
      * *[!UICONTROL Store View]*: *[!UICONTROL Default Store View]*
   1. 2 つ目の web サイト/ストア表示に別の条件を作成します。
1. **[!UICONTROL Stores]**/**[!UICONTROL All Stores]** に移動して、デフォルトの web サイトを変更します。 2 つ目の Web サイトをクリックし、「*[!UICONTROL Set as Default]*」をオンにして保存します。
1. 次を使用してキャッシュをクリアします。

   ```bash
   bin/magento cache:clear
   ```

1. ストアフロントに移動し、商品を買い物かごに追加します。 チェックアウトに進み、注文します（利用条件に同意するための支払い方法ステップにチェックボックスが表示されます）。
1. 注文後に管理者に戻り、デフォルトの web サイトを元のメインの web サイトに変更して保存します。
1. キャッシュをクリアする：

   ```bash
   bin/magento cache:clear
   ```

1. 次のコマンドを実行して、キューコンシューマーを起動します。

   ```bash
   bin/magento queue:cons:start placeOrderProcessor
   ```

<u> 期待される結果 </u>:

注文が履行されました。自動的には拒否されません。

<u> 実際の結果 </u>:

注文ステータスは *却下* で、次のコメントが付きます。

*注文は行われませんでした。 まず、利用規約に同意してから、もう一度注文してみてください。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
