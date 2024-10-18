---
title: Adobe Commerce サポートナレッジベース
description: Commerce Store のトラブルシューティングと管理に必要なすべての知識。
exl-id: feacf38f-2803-4170-a64f-5d7c4567432d
feature: Support
role: Admin
source-git-commit: 607b835da518536196654734f62d78d095099476
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# Adobe Commerce サポートナレッジベース

>[!NOTE]
>
>Adobe Commerce サポートナレッジベースガイドは間もなく再構築され、そのコンテンツはAdobe Experience League内の他の場所に移動されます。 それまでの間、このガイドの内容を引き続き維持および更新します。

![ ナレッジベースのホームページ ](../help/assets/knowledge-base-home-page-cover.jpg){width="100%"}

このナレッジベースの情報は、[Adobe Commerce Developer Documentation](https://developer.adobe.com/commerce/docs)、[Adobe Commerce マーチャントガイド ](https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html) およびその他のAdobe Commerceのパブリケーションを補完するように設計されています。 公式ドキュメントでは、トラブルシューティングとベストプラクティス、ホストのお知らせ、よくある質問への回答および（何らかの理由で）記載されていない具体的なシナリオについて説明します。

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
    <a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25075"> セキュリティスキャンツールが「サーバーが 2FA を使用しているかどうかを判断できません」を返す：</a> エラーを解決するには、<code>Magento_TwoFactorAuth</code> モジュールが無効になっているかどうかを確認します。 チェックに合格するには、通常、有効にする必要があります。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-51/acsd-60632-address-saved-on-every-order-attempt">ACSD-60632：注文の試行のたびに保存されるアドレス：</a> ACSD-60632 パッチは、注文が正常に作成されたかどうかに関係なく、注文の試行のたびに新しいアドレスが保存される問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.51 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-51/acsd-60326-graphql-query-error-customer-return-status">ACSD-60326：カスタマーリターンのステータスに関するGraphQL クエリで、次のエラーが発生します。</a> ACSD-60326 パッチは、カスタマーリターンのステータスに関するGraphQL クエリでエラーが発生する問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.51 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-52/acsd-59925-sorting-items-in-media-gallery">ACSD-59925:Media Gallery 内の項目をGraphQL内の位置で並べ替える：</a> ACSD-59925 パッチは、Media Gallery 内の項目が位置で並べ替えられず、誤った表示順になる問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.52 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-52/acsd-61322-products-not-assigned-to-shared-catalogue">ACSD-61322：共有カタログに割り当てられていない製品が XML サイトマップに含まれる：</a> ACSD-61322 パッチは、デフォルト（一般）グループの共有カタログに割り当てられていない製品/カテゴリが、XML サイトマップに引き続き含まれる問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.52 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-52/acsd-60590-optimized-bestseller-report-generation">ACSD-60590：ベストセラー集計日別レポート生成のパフォーマンスの強化：</a> ACSD-60590 パッチは、ベストセラー集計日別レポートが大量の注文に対して生成されるまでに多くの時間がかかる問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.52 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-52/acsd-59865-cart-price-rule-fix-for-insufficient-quantity-issue">ACSD-59865：買い物かご価格ルールで、製品数量が不十分なために以前のルールをキャンセルできない：</a>ACSD-59865 パッチは、<em> 割引数量ステップ </em> 値が <em> 固定金額割引 </em>、<em> 製品価格割引の割合 </em>、および <em> 購入 X と Y</em> 買い物かご価格ルールで、以前のルールのアクションがキャンセルされなくなる問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.52 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/error-when-filtering-orders-in-admin">Error when filtering orders in the Admin:</a> この記事では、管理画面で注文を日付別にフィルターしようとするとエラーが発生するAdobe Commerceの問題に対して、次のメッセージを表示します。<em>Integrity constraint violation: 1052 Column 'created_at' where 句があいまいである </em>。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25030">Adobe Commerce：コンテンツセキュリティポリシー（CSP）制限モードのチェックアウトページで発生するインラインJavaScriptの問題：</a> この記事では、（CSP 制限モード <strong> が有効な場合に、チェックアウト時にAdobe Commerce 2.4.7 のAdobe Commerce管理およびGoogle タグマネージャーで追加されたカスタムJavaScriptで発生する問題に関する説明と解決策について説明し </strong> す。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-51/acsd-61195-empty-cart-on-final-graphql-page">ACSD-61195：買い物かごGraphQLリクエストで、最終ページに商品を返すことができない：</a> ACSD-61195 パッチは、買い物かごGraphQLリクエストの最後のページで買い物かご商品が返されない問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.51 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-50/acsd-59514-forms-in-admin-with-page-builder-throw-error-in-browser-console">ACSD-59514：ページビルダーを使用した管理者のFormsがブラウザーコンソールでスローするエラー：</a>ACSD-59514 パッチは、ページビルダーを使用している管理者のフォームが、フォームの送信後にブラウザーコンソールで <em> ページビルダーがロックを解除せずに 5 秒間レンダリング中 </em> エラーをスローし、変更を保存できない問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.50 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-51/acsd-60538-if-product-is-disabled-attributes-dont-show">ACSD-60538：商品が <em> すべてのストア表示 </em> で無効になっている場合、属性が正しく表示されない：</a>ACSD-60538 パッチは、<em> すべてのストア表示 </em> で無効になっており、特定のストア表示範囲でのみ有効になっている場合、GraphQL レスポンスで商品の属性が正しく表示されず、商品が正しく表示されない問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.51 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/patches-available-in-qpt/v1-1-50/acsd-58352-return-attribute-labels-for-the-default-store-are-returned-via-graphql-api">ACSD-58352：デフォルトストアの戻り属性ラベルがGraphQL API を使用して返される：</a> ACSD-58352 パッチは、リクエストヘッダーでデフォルト以外のストアビューが指定されている場合に、GraphQL API を使用してデフォルトストアの戻り属性ラベルが返される問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.50 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href = "https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-24983"> アカウントの切り替え <em></em> ドロップダウンがアカウントにありません。</a> この記事では、Adobe Commerceの問題の解決策を説明します。この問題では、アカウントの <em> アカウントの切り替え </em> ドロップダウンが見つからず、マーチャントに代わってチケットを送信するアクセス権を失っています。
    </td>
    <td>新しい記事</td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>  
    <td>
    <a href = "https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-49/acsd-56979-product-images-removed-after-staging-update-deleted">ACSD-56979：ステージング更新プログラムの削除後に製品画像が削除されました：</a>ACSD-56979 パッチは、ステージング更新プログラムを削除した後に製品画像が削除される問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.49 がインストールされている場合に使用できます。  
    </td>
    <td>新しい記事</td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-50/acsd-48210-store-view-specific-scope-attribute-overrides-global-values">ACSD-48210：ストアビュー特定のスコープ属性がグローバル値を上書きする：</a> ACSD-48210 パッチは、特定のストアビュー内の <em>Website Scope</em> 属性を更新するときに、グローバルスコープの属性値を上書きする問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.50 がインストールされている場合に使用できます。 
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-50/acsd-59280-fix-for-reflection-union-type-error">ACSD-59280:2.4.4-pX インストールで ReflectionUnionType::getName （） エラーが発生する：</a> ACSD-59280 パッチは、2.4.4-pX バージョンのインストール中に未定義メソッド <code>ReflectionUnionType::getName()</code> エラーの呼び出しが発生する問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.50 がインストールされている場合に使用できます。 
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-50/acsd-54887-customer-shopping-cart-gets-cleared-after-session-expiry">ACSD-54887：顧客セッションの有効期限が切れた後、顧客の買い物かごがクリアされる：</a> ACSD-54887 パッチは、<em> 永続的な買い物かご </em> が有効になっている顧客セッションの有効期限が切れた後に、顧客の買い物かごがクリアされる問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.50 がインストールされている場合に使用できます。 
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-50/acsd-60303-admin-order-placement-fix">ACSD-60303:HTMLの縮小が有効な状態で、管理者の注文の配置に関する問題が解決されました：</a> ACSD-60303 パッチは、HTMLの縮小が有効な状態で、管理者からの注文が配置できない問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.50 がインストールされている場合に使用できます。 
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-49/acsd-57045-url-rewrites-cause-infinite-page-looping-after-website-root-unchecked-hierarchy">ACSD-57045：階層からチェックを外した <em>Website Root</em> 後に URL の書き換えによって無限ページループが発生する：</a> ACSD-57045 パッチは、<em>Website Root</em> を階層からチェックを外した後に URL の書き換えによって無限ページループが発生する問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.49 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-49/ascd-58446-deleting-a-team-with-child-users-or-teams-via-graphql-gives-an-uninformative-error-message">ACSD-58446:GraphQLを使用して子ユーザーまたはチームを含むチームを削除すると、非情報エラーメッセージが表示される：</a> ACSD-58446 パッチは、GraphQLで子ユーザーまたはチームを含むチームを削除すると、UI に矛盾する非情報エラーメッセージが返されるAdobe Commerceの問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.49 がインストールされている場合に使用できます。 
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-49/acsd-58375-wrong-youtube-api-key-configuration-causes-an-error-when-adding-a-youtube-video-at-the-store-view-level">ACSD-58735：誤って設定されたYouTube API キーが、ストアビューレベルでビデオを追加する際にエラーが発生する：</a> ACSD-58735 パッチは、誤ったYouTube API キーの設定が、ストアビューレベルでYouTube ビデオを追加する際にエラーが発生する問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.49 がインストールされている場合に使用できます。 
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-49/acsd-57086-orders-placed-from-non-default-websites-with-terms-conditions-processed-incorrectly">ACSD-57086：利用条件が有効なデフォルト以外の web サイトからの注文が正しく処理されない：</a> ACSD-57086 パッチは、利用条件が有効なデフォルト以外の web サイトから注文が正しく処理されない問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.49 がインストールされている場合に使用できます。 
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-50/acsd-58141-phpsessid-regenerates-on-post-requests-for-logged-in-customers-with-l2-redis-cache-enabled">ACSD-58141:L2 Redis キャッシュが有効な場合、ログイン中のお客様のPOSTリクエストで PHPSESSID が再生成されます。</a> ACSD-58141 パッチは、L2 Redis キャッシュが有効な場合、ログイン中のお客様のPOSTリクエストで PHPSESSID が再生成され、管理者から更新される問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.50 がインストールされている場合に使用できます。 
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-50/acsd-58790-fixes-pinch-to-zoom-functionality-on-the-product-detail-page-images-in-mobile-view-on-chrome">ACSD-58790:Chromeのモバイルビューの商品詳細ページ画像で、ピンチからズーム機能が修正されました：</a> ACSD-58790 パッチは、Chromeのモバイルビューの画像が期待どおりにズームされなかったAdobe Commerceの問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.50 がインストールされている場合に使用できます。 
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>

<tr>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/patches/v1-1-50/acsd-58442-fixes-issue-devices-768px-mobile-view-instead-desktop">ACSD-58442：幅 768 px のデバイスがモバイルとして扱われ、メニューとヘッダーがデスクトップではなくモバイルビューに読み込まれる問題を修正しました。</a> ACSD-58442 パッチは、幅 768 px のデバイスがモバイルとして扱われ、メニューとヘッダーがデスクトップではなくモバイルビューに読み込まれるAdobe Commerceの問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.50 がインストールされている場合に使用できます。
    </td>
    <td>新しい記事 </td>
    <td>2024 年 10 月 17 日（Pt）</td>
  </tr>
</table>
