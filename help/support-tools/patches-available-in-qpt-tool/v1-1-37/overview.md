---
title: '概要： [!DNL Quality Patches Tool] （QPT） v1.1.37'
description: このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.37。
feature: Tools and External Services
role: Admin, Developer
exl-id: 4ccdba38-8171-4cc4-b8ef-d2c53dec0b47
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 概要： [!DNL Quality Patches Tool] （QPT） v1.1.37

このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.37。

QPT v1.1.37 には、次のパッチが含まれています。

1. **ACSD-52613**：に対して更新がおこなわれなくてもキャッシュとインデックスが更新される問題を修正しました `Inventory_source` rest API による項目。
1. **ACSD-51884**：サイズ変更コマンドを実行すると、製品画像のキャッシュパスが正しくなくなる問題を修正しました。
1. **ACSD-53628**:CSV 販売注文レポートに間違った特殊文字が表示される問題を修正しました。
1. **ACSD-49843**：で注文した項目がオンライン支払い方法によって自動請求された後、製品のダウンロードのリンクが使用できなくなる問題を修正しました *[!UICONTROL Payment Action]* = *[!UICONTROL Sale]* の設定が有効になっています。
1. **ACSD-53148**：設定可能な同じ商品を買い物かごに追加するためにGraphQLで並行して実行された 2 つのリクエストの結果、同じ商品 SKU を持つ 2 つの異なる商品が買い物かごに含まれていた問題を修正しました。
1. **ACSD-47054**：プレビューのインデックス再作成がすべてのストアに対してインデックス再作成を実行して、遅延が発生する問題を修正しました。
1. **ACSD-52606**：エラーメッセージが表示される問題を修正します *注文を受け取る準備ができていません* ユーザーがクリックしたときに表示されます。 **[!UICONTROL Notify Order is Ready for Pickup]**.
1. **ACSD-51574**：画像を同じ名前の別の画像に置き換えた後、フロントエンドで画像が更新されない問題を修正しました。
1. **ACSD-53728**：製品の EAV インデクサーの完了に時間がかかる問題を修正しました。
1. **ACSD-53979**：ようこそメッセージに一重引用符が含まれている場合、ホームページで発生する JS の問題を修正します。
1. **ACSD-52143**：製品の読み込み後にカスタムオプションが削除される問題を修正しました。
1. **ACSD-53750**：を修正します *壊れたパイプまたは閉じた接続* マルチスレッド中のエラー `catalog_product_price` 再インデックス。

左側のメニューを使用して、特定のパッチページに移動します。