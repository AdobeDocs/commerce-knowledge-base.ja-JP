---
title: 顧客グループ名、セグメントおよびプロモーションルール情報が、 [!DNL GraphQL] の方法で公開される。
description: この記事では、 [!DNL GraphQL] を介して顧客グループ名、顧客セグメントおよびプロモーションルール情報が公開されるのを防ぐためのホットフィックスを提供します。
feature: GraphQL
role: Admin, Developer
source-git-commit: f32085c80c9dbce513dad15ebf5f77a0e6398466
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# [!DNL GraphQL] を介して公開される顧客グループ名、セグメントおよびプロモーションルール情報

この記事では、[!DNL GraphQL] を介して顧客グループ名、顧客セグメントおよびプロモーションルール情報が公開されるのを防ぐためのホットフィックスを提供します。 この問題は、Adobe Commerce 2.4.8-p1 で修正される予定です。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.8

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.8

## 問題

[!UICONTROL Storefront Personalization Drop-ins] では、顧客グループ名、セグメント、買い物かご、カタログルールなどの基本情報を表示する新しい [!DNL GraphQL] ミューテーションが導入されました。 ただし、名前に含まれている場合、オファーの詳細やクーポンコードなどの機密データが公開される可能性があります。

### 再現手順

#### ケース I:[!UICONTROL Catalog Rule]

1. *管理者* サイドバーで、**[!UICONTROL Marketing]**/**[!UICONTROL Catalog Price Rule]**/**[!UICONTROL Add New Rule]** に移動します。
1. ルール条件（製品属性やカテゴリなど）を定義します。
1. ルールを保存して適用します。
1. 製品がルール条件を満たしていることを確認します。
1. 次の [!DNL GraphQL] クエリを実行して、すべてのルールを取得します。

   ```
   query {
       allCatalogRules {
           name
       }
   }
   ```

1. 製品をクエリして、ルールが適用されるかどうかを確認します。

   ```
   query {
       products(filter: { sku: { eq: "product-sku" } }) {
           items {
               name
               rules {
                   name
               }
           }
       }
   }
   ```

#### ケース II:[!UICONTROL Cart Rule]

1. *管理者* サイドバーで、**[!UICONTROL Marketing]**/**[!UICONTROL Cart Price Rule]**/**[!UICONTROL Add New Rule]** に移動します。
1. 条件（買い物かごの最小値や顧客グループなど）を設定します。
1. ルールを保存して適用します。
1. 商品を買い物かごに追加して、ルールをトリガーします。
1. [!DNL GraphQL] を使用して、すべての買い物かごルールを確認します。

   ```
   query {
       allCartRules {
           name
       }
   }
   ```

1. アクティブな買い物かごにルールが適用されているかどうかを確認します。

   ```
   query {
       cart(cart_id: "your-cart-id") {
           rules {
               name
           }
       }
   }
   ```

#### ケース III: [!UICONTROL Customer Group]

1. *管理者* サイドバーで、**[!UICONTROL Customers]**/**[!UICONTROL Customer Groups]** に移動します。
1. 必要なグループが存在することを確認します。
1. [!DNL GraphQL] を使用して、すべてのグループを取得します。

   ```
   query {
       allCustomerGroups {
           name
       }
   }
   ```

1. 顧客/ゲストのグループを確認します。

   ```
   query {
       customerGroup {
           name
       }
   }
   ```

#### ケース IV:[!UICONTROL Customer Segment] （Adobe Commerceのみ）

1. *管理者* サイドバーで、**[!UICONTROL Customers]**/**[!UICONTROL Customer Segments]** → **[!UICONTROL Add Segment]** に移動します。
1. 顧客ベースの条件（注文、買い物かごの中身など）を定義する。
1. 適用可能な範囲（*[!UICONTROL Visitor]*、*[!UICONTROL Registered]* またはその両方）を割り当てます。
1. 条件がテスト顧客に一致することを確認します。
1. [!DNL GraphQL] を使用して、すべてのセグメントを確認します。

   ```
   query {
       allCustomerSegments {
           name
           apply_to
       }
   }
   ```

1. 買い物かごに適用されたセグメントを検証します。

   ```
   query {
       customerSegments(cartId: "your-cart-id") {
           name
       }
   }
   ```

<u> 期待される結果 </u>:

顧客グループ名、セグメント名およびプロモーションルール情報は、[!DNL GraphQL] では公開されません。

<u> 実際の結果 </u>:

顧客グループの名前、セグメントおよびプロモーションルール情報は、[!DNL GraphQL] を通じて公開されます。

## 解決策

Adobe Commerceのバージョンに応じて、添付されているパッチを適用します。

* Adobe Commerce バージョン 2.4.8 の場合：

   * [LYNX-839_CE_2.4.8.patch](assets/LYNX-839_CE_2.4.8.patch.zip)
   * [LYNX-839_EE_2.4.8.patch](assets/LYNX-839_EE_2.4.8.patch.zip)

* Open Source バージョン 2.4.8 の [!DNL Magento] 合：

   * [LYNX-839_CE_2.4.8.patch](assets/LYNX-839_CE_2.4.8.patch.zip)
