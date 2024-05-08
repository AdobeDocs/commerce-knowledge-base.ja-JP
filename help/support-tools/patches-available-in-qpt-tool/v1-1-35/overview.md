---
title: '概要： [!DNL Quality Patches Tool] （QPT） v1.1.35'
description: このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.35.
feature: Tools and External Services
role: Admin
exl-id: 46228690-44ce-462f-b700-1aea6fa0eeab
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# 概要： [!DNL Quality Patches Tool] （QPT） v1.1.35

このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.35.

QPT v1.1.35 には、次のパッチが含まれています。

1. **ACSD-51899**：チェックアウト配送ステップのデフォルトの配送先住所に、以前に選択した店舗の集荷先住所が自動入力される問題を修正しました。
1. **ACSD-52041**：エラーメッセージが表示される問題を修正します。 *[エラー] [!DNL Page Builder] は、ロックを解除せずに 5 秒間レンダリングしていました*. 次に表示： [!DNL Chrome] で編集したコンテンツを保存する際のブラウザー [!DNL Page Builder].
1. **ACSD-52095**：が発生した問題を修正します `manage_stock` 製品の書き出し後、CSV ファイルの値が正しく 0 に設定されていませんでした。
1. **ACSD-51358**：終了日を指定せずにスケジュール済み更新を削除すると、同じエンティティで他のスケジュール済み更新が削除される問題を修正しました。
1. **ACSD-48070**：スケジュールされた更新を編集すると例外がトリガーされる問題を修正しました。
1. **ACSD-51890**：が発生した問題を修正します [!UICONTROL Submit review] ボタンは、次の操作を行わずに複数回クリックできます [!DNL Google] reCAPTCHA v3 検証。
1. **ACSD-51984**：チェックされていない問題を修正します *デフォルト値およびデフォルト以外の製品フィールド値の使用* は、2 番目の web サイト、ストア、ストア表示には保存されません。
1. **ACSD-52398**：エラーを修正します *リクエストされた数量は使用できません* この問題は、ストアフロントで買い物かごにバンドルされた製品の数量を更新しようとした場合に発生します。
1. **ACSD-52786**：特定の SKU で始まるすべての製品にカタログルール条件 SKU が適用される問題を修正しました。
1. **ACSD-52921**：カートに在庫切れの設定可能な商品がある場合に、GraphQLからカートの詳細をリクエストすると内部エラーが発生する問題を修正しました。
1. **ACSD-51683**:GraphQLを使用してカスタマイズ可能なオプションを買い物かごに追加できない問題を修正しました。
1. **ACSD-52133**：アップグレード後にカスタマーアカウントを保存できない問題を修正しました。
1. **ACSD-52202**：注文のフルフィルメントでデフォルト以外の在庫が 0 数量に変更された場合に、デフォルト在庫の販売可能数量が誤って 0 に変更される問題を修正します。
1. **ACSD-51265**：の問題を修正しました `catalog_product_price` システムにバンドルされた製品が多すぎる場合のインデックス再作成のパフォーマンス。
1. **ACSD-52831**：次の場合に、顧客が交渉可能な見積依頼を送信できない問題を修正しました [!DNL Google reCAPTCHA v3 Invisible] が有効になっています。
1. **ACSD-51845**：階層価格と異なる属性セットを持つ後続の製品を非同期の一括 REST API で更新できない問題を修正しました。
1. **ACSD-52815**：デフォルト以外のソースの数量フィールドに対する入力で、デフォルトの在庫の 8 桁とは異なり、最大 6 桁しかサポートしない問題を修正しました。
1. **ACSD-51149**：の問題を修正します [!UICONTROL Scheduled ImportExport] が有効の場合 [!UICONTROL Catalog Permissions] インデクサーを無効化してから、cron によるキャッシュのフラッシュを行います。
1. **ACSD-50815**：新しいバンドル製品オプションに単純な製品の 10 進数の数量が使用できない問題を修正しました。
1. **ACSD-52399**：設定可能な製品オプションの販売可能数量が 0 と表示される問題を修正しました *在庫あり* 製品ページに移動します。

左側のメニューを使用して、特定のパッチページに移動します。