---
title: 「MDVA-41229：設定可能な製品の読み込み後、バックエンドで使用可能な画像がフロントエンドに表示されない」
description: MDVA-41229 パッチは、設定可能な製品の読み込み後に、バックエンドで利用可能な画像がフロントエンドに表示されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-41229。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 69d7374f-9f8b-4ec4-8a7f-135ee06135a3
feature: Data Import/Export, Configuration, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# MDVA-41229：設定可能な製品の読み込み後、バックエンドで使用可能な画像がフロントエンドに表示されない

MDVA-41229 パッチは、設定可能な製品の読み込み後に、バックエンドで利用可能な画像がフロントエンドに表示されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.12 がインストールされている場合に使用できます。 パッチ ID は MDVA-41229。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2-p2 および 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な製品の読み込み後、バックエンドで使用可能な画像はフロントエンドに表示されません。

<u> 再現手順 </u>:

1. クリーンなAdobe Commerceをインストールします。
1. **ストア**/**属性**/**製品**/**新規属性を追加** に移動して、以下の設定を使用してカスタム属性を追加します。

   * プロパティ：
      * 属性プロパティ：

         * デフォルトのラベル：サイズを設定
         * 店舗所有者のカタログ入力タイプ：テキスト スウォッチ
         * 必要な値：なし
         * 製品プレビュー画像を更新：はい

      * スウォッチの管理（属性の値）:

        | デフォルト | 管理スウォッチ | 管理者の説明 | デフォルトのストア表示スウォッチ | デフォルトのストア表示の説明 |
        |---|---|---|---|---|
        | なし | 4 | 4 | 4 | 4 |
        | なし | 24 | 24 | 24 | 24 |
        | なし | 30 | 30 | 30 | 30 |
        | なし | 60 | 60 | 60 | 60 |
        | なし | 68 | 68 | 68 | 68 |

      * 詳細属性プロパティ：

         * 属性コード：set_size
         * 範囲：グローバル
         * 一意の値：いいえ
         * ストア所有者の入力検証：なし
         * 列に追加オプション：いいえ
         * フィルターオプションで使用：なし

   * ラベルを管理：

      * タイトル（サイズ、色など）の管理

         * デフォルトのストア表示：サイズを設定

   * ストアフロントのプロパティ：

      * 検索で使用：はい
      * 検索の重み付け：1
      * 詳細検索に表示：いいえ
      * ストアフロントで同等：はい
      * レイヤナビゲーションでの使用：フィルタリング可能（結果を含む）
      * 検索結果での使用階層ナビゲーション：はい
      * プロモルール条件に使用：いいえ
      * ストアフロントのカタログページに表示：はい
      * 製品リストでの使用可：はい
      * 製品リストでの並べ替えに使用：いいえ

1. この属性を製品詳細グループ（**ストア**/**属性**/**属性セット**）内のデフォルト属性セットに追加します。
1. Adobe Commerce ルートディレクトリ内の var フォルダーに設定された画像をダウンロードします。
1. **システム**/**データ転送**/に移動し、以下のオプションを使用してファイルを読み込みます。

   * 読み込み設定：

      * エンティティタイプ：Products

   * 読み込み動作：

      * 読み込みの動作：追加/更新
      * 検証方法：エラー時に停止
      * 許可されたエラー数：1
      * フィールド区切り記号：`;`
      * 複数の値の区切り記号：`,`
      * 属性値の定数：EMPTYVALUE
      * フィールドの囲い文字：オフ

   * インポートするファイル：

      * 読み込むファイルを選択
      * 画像ファイルディレクトリ：空のままにします

1. ストアフロントに移動してページ `/product-set.html` 移動し、異なるセットサイズを切り替えます。 セットサイズ 24 の場合、ギャラリーはありません。

<u> 期待される結果 </u>:

設定可能な製品内のすべてのシンプルな製品のギャラリーは、関連するすべての画像で表示されます。

<u> 実際の結果 </u>:

商品のギャラリーはありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
