---
title: Adobe Commerce サポートナレッジベース
description: Commerce Store のトラブルシューティングと管理に必要なすべての知識。
exl-id: feacf38f-2803-4170-a64f-5d7c4567432d
feature: Support
role: Admin
source-git-commit: 6d22ea4725249df1528625672be405464b1411e8
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Adobe Commerce サポートナレッジベース

>[!NOTE]
>
>Adobe Commerce サポートナレッジベースガイドは間もなく再構築され、そのコンテンツはAdobe Experience League内の他の場所に移動されます。 それまでの間、このガイドの内容を引き続き維持および更新します。

![ ナレッジベースのホームページ ](../help/assets/knowledge-base-home-page-cover.jpg){width="100%"}

このナレッジベースの情報は、[Adobe Commerce Developer Documentation](https://developer.adobe.com/commerce/docs)、[Adobe Commerce マーチャントガイド ](https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html?lang=ja) およびその他のAdobe Commerceのパブリケーションを補完するように設計されています。 公式ドキュメントでは、トラブルシューティングとベストプラクティス、ホストのお知らせ、よくある質問への回答および（何らかの理由で）記載されていない具体的なシナリオについて説明します。

## このナレッジベースには何がありますか？

| カテゴリ | 説明 |
| --- | --- |
| [ サポートツール ](/help/support-tools/overview.md) | Adobe Commerceが提供する様々なサポートツールを使用して、e コマースストアのエクスペリエンスを向上させることができます。 パーソナライズされたベストプラクティス、診断および監視ツール、サイトに関する最も関連性の高い情報を提供します。 |
| [ 発表 ](/help/announcements/overview.md) | Adobe Commerce チームから重要なアップデートを入手してください。 |
| [ トラブルシューティング ](/help/troubleshooting/overview.md) | セルフサービスソリューションおよびパッチについては、Adobe Commerce サポートチームまでお問い合わせください。 |
| [ ヘルプセンターユーザーガイド ](/help/help-center-guide/help-center/magento-help-center-user-guide.md) | サポートチケットの管理、共有アクセスの付与、ナレッジベースの効果的な参照方法について説明します。 |
| [ ハウツー ](/help/how-to/overview.md) | Adobe Commerce サポートチームから明確な手順を段階的に取得します。 |
| [FAQ](/help/faq/overview.md) | Adobe Commerceのポリシー、戦略、Adobe Commerce機能の詳細に関するよくある質問を紹介します。 |

## 新機能

<table style="width:100%">
  <tr>
    <th style="width:70%">説明</th>
    <th style="width:15%">タイプ</th>
    <th style="width:15%">日付</th>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25301">Adobe Commerceでの PHP 8.2 から 8.3 へのアップグレードに関する [!DNL New Relic] Agent の問題を解決する：</a> PHP を 8.2 から 8.3 にアップグレードすると、Adobe Commerce環境で [!DNL New Relic] Agent が動作しなくなることがあります。 この問題は、ステージング環境と実稼動環境で発生しています。 この記事では、この問題のトラブルシューティングと解決の手順を説明します。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    パッチが既に適用されている場合でも、<a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25321">[!DNL Security Scan Tool] は「APSByy-xx security updates available」を返します。</a> パッチを既に適用しているにもかかわらず、Adobe CommerceおよびMagento Open Sourceで利用できる APSByy-xx セキュリティアップデートが [!DNL Security Scan Tool] にレポートされます。 この通知は無視してかまいません。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-54/acsd-61845-error-occurs-for-requests-with-text-html-accept-header">ACSD-61845: text/html accept ヘッダーを含むリクエストでエラーが発生します：</a> ACSD-61845 パッチは、text/html accept ヘッダーのみを含む HTTP リクエストが、応答処理でのメディアタイプの不一致に起因して 500 エラーを引き起こす問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.54 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-54/acsd-61200-fixes-discount-tax-compensation-in-sales-total-calculations">ACSD-61200：売上合計の計算における割引税報酬の誤り：</a>ACSD-61200 パッチにより、合計金額および合計金額実績計算に割引税報酬金額および出荷割引税報酬金額が欠落し、受注データとクーポン・レポート・データの間に不一致が生じる問題が修正されます。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.54 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-54/acsd-61199-cms-page-hierarchy-tab-doesnt-display-proper-tree-structure">ACSD-61199:CMSページの「[!UICONTROL Hierarchy]」タブに適切なツリー構造が表示されない：</a> ACSD-61199 パッチは、既存の階層を使用してCMSページを編集したときに、CMSページの「[!UICONTROL Hierarchy]」タブに適切なツリー構造が表示されない問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.54 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-53/acsd-60804-editing-customer-linked-to-deleted-company-causes-error">ACSD-60804：削除された会社に関連付けられた顧客を編集すると、次のエラーが発生します。</a> ACSD-60804 パッチは、削除された会社に関連付けられた顧客を編集すると、エラー <em> メンバー関数 getSuperUserId （）の呼び出しが null で </em> が発生する問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.53 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-54/acsd-61522-email-in-name-fields-sends-invalid-order-confirmations">ACSD-61522:[!UICONTROL First] および [!UICONTROL Last Name] フィールドのメールアドレスから無効な注文確認が送信される：</a> ACSD-61522 パッチは、ゲスト顧客の [!UICONTROL First Name] および [!UICONTROL Last Name] フィールドにメールアドレスを入力すると、無効な注文確認メールが送信される問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.54 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-54/acsd-62485-async-operations-all-consumer-stops-working-when-company-is-created">ACSD-62485：会社が作成されると <code>async.operations.all</code> コンシューマーの動作が停止する：</a> ACSD-62485 パッチは、B2B 会社が作成されると <code>async.operations.all</code> コンシューマーの動作が停止する問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.54 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-52/acsd-60684-graphql-product-sorting-by-multiple-fields-does-not-work-as-expected">ACSD-60684：複数のフィールドで並べ替えたGraphQL製品が、期待どおりに動作しない：</a> ACSD-60684 パッチは、変数で並べ替えを渡す際にGraphQL製品が複数のフィールドで並べ替えが機能しない問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.52 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-53/acsd-61553-cart-price-rule-discounts-are-incorrectly-calculated-when-multiple-discounts-with-different-priorities-are-applied">ACSD-61553：異なる優先度の複数のディスカウントが適用されると、[!UICONTROL Cart Price Rule] が誤って計算されます。</a> ACSD-61553 パッチは、異なる優先度の複数のディスカウントが適用されると [!UICONTROL Cart Price Rule] が誤って計算される問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.53 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-55/acsd-58383-duplicate-credit-memos-from-simultaneous-refund-requests-via-rest-api">ACSD-58383 Adobe Commerce パッチ：REST API を使用した同時払い戻しリクエストからクレジットメモを複製：</a> ACSD-58383 パッチは、同時に実行される 2 つの同一のリクエストで REST API を使用して払い戻しを行うと、クレジットメモが重複する問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.55 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-55/acsd-58471-dynamic-content-fails-load-product-detail-page">ACSD-58471：関連するカタログ価格ルールがスケジュールされている場合、動的コンテンツを製品詳細ページに読み込めない：</a> ACSD-58471 パッチは、関連するカタログ価格ルールがスケジュールされている場合、動的コンテンツを製品詳細ページに読み込めない問題を解決します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.55 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-55/acsd-58735-restricted-admin-cant-view-abandoned-shopping-carts">ACSD-58735：制限付き管理者は、関連する web サイトの顧客アカウントで放棄された買い物かごを表示できません：</a> ACSD-58735 パッチは、制限付き役割を持つ管理者ユーザーが、<strong>[!UICONTROL Commerce Admin]</strong> &gt; <strong>[!UICONTROL Reports]</strong> &gt; <strong>[!UICONTROL Abandoned Carts]</strong> &gt; <strong>[!UICONTROL Select Cart]</strong> &gt; <strong>[!UICONTROL Shopping Cart]</strong> タブから放棄された顧客の買い物かごを表示できない問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.55 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 12 月 5 日（Pt）</td>
  </tr>
</table>
