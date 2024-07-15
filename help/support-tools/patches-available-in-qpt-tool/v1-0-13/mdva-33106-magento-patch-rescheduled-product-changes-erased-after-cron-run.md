---
title: 「MDVA-33106 パッチ：再スケジュールされた製品の変更が cron の実行後に消去される」
description: MDVA-33106 パッチを適用すると、再スケジュールされた製品の変更が cron の後で消去される問題が修正されます
exl-id: be32982c-796c-4069-ad70-37b5124ffb56
feature: Products
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# MDVA-33106 パッチ：再スケジュールされた製品変更が cron の実行後に消去される

MDVA-33106 パッチを適用すると、再スケジュールされた製品の変更が cron の後で消去される問題が修正されます

```bash
bin/magento cron:run
```

コマンドが実行されます。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.13 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.2 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. Commerce管理者で、**カタログ**/**製品** に移動し、「編集」をクリックします。 **Price** の値、例えば *9.99* に注目してください。
1. **新規更新をスケジュール** をクリックし、詳細を入力します。
   * 更新名は重要ではありません。
   * 開始日と終了日には+1 年後の日付を設定してください。
   * 「価格」を *1.99* に設定します。
   * 変更を保存します。
1. コンテンツのステージングダッシュボードに移動し、グリッド表示を選択して、上記のスケジュールされた一致が表示されるかどうかを確認します。
1. スケジュールされた更新の横にある「編集アクション」を選択します。 データは、上記と引き続き一致する必要があります。
1. スケジュールされた日付を近い日付に変更します。 今から+1 年の代わりに、+1 週間または+1 か月に変更します。
1. 変更を保存し、ステージングダッシュボードで日付が更新されているかどうかを確認します。
1. cron ジョブが実行されるのを待ちます。
1. スケジュールされた変更で「編集」を再度クリックし、価格を確認します。

<u> 期待される結果 </u>:

価格は 1.99 です。

<u> 実際の結果 </u>:

価格は 9.99 です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
