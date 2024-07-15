---
title: 制限モードでのストアフロントのチェックアウトページ [!UICONTROL CSP] トラブルシューティング
description: この記事では、CSP 制限モードでチェックアウトページを表示している際に発生する可能性のあるエラーについて説明し、それらのエラーを修正するソリューションを提供します。
feature: Checkout,Security,Orders,Payments
role: Developer
exl-id: fb92b75d-c88b-4810-a309-d6ab38485e86
source-git-commit: 6d0c4ea9576440d66be3b8053a6e362b8ac0ebcb
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# 制限モードでのストアフロントのチェックアウトページ [!UICONTROL CSP] トラブルシューティング

ここでは、**[!UICONTROL CSP restricted mode]** でチェックアウトページを表示している際に発生するAdobe Commerce 2.4.7 の問題と、「*Refused to execute inline script that it permissions to following Content Security Policy directive: &quot;script-src ...*&quot;」というエラーメッセージについて説明します。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure、Adobe Commerce オンプレミス、およびMagento Open Source:

* 2.4.7
* 2.4.6-pX
* 2.4.5-pX
* 2.4.4-pX

## 問題 – ストアフロントのチェックアウトページが壊れているか、読み込めません

**ストアフロントのチェックアウト** ページが壊れているか、読み込めません。その際、「*インラインスクリプトの実行を拒否しました：ブラウザーコンソールログに表示されるコンテンツセキュリティポリシーディレクティブ「script-src ...*」エラーメッセージに違反しているためです。

<u> 再現手順 </u>:

1. ストアフロントに移動します。
1. 買い物かごに商品を追加し、チェックアウトに進みます。

<u> 期待される結果 </u>:

チェックアウトページが正常に読み込まれる。

<u> 実際の結果 </u>:

チェックアウトページが空白であるか、コンポーネントがありません。 「*コンテンツセキュリティポリシーディレクティブ「script-src ...*」に違反しているので、インラインスクリプトの実行を拒否しました」という [!DNL JS] エラーがブラウザーコンソールログに表示されます

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、**[!UICONTROL CSP]** は、デフォルトで、ストアフロントおよび管理領域の支払いページ用に `restrict-mode` で設定され、その他のすべてのページ用に `report-only` モードで設定されます。
対応する **[!UICONTROL CSP]** ヘッダーには、支払いページの `script-src` ディレクティブ内に `unsafe-inline` キーワードが含まれていません。 また、[!DNL whitelisted] インラインスクリプトのみ使用できます。

### 解決策

次の理由で特定のスクリプトがブロックされると、ブラウザーエラーが表示される場合が **[!UICONTROL CSP]** ります。

`Refused to execute inline script because it violates the following Content Security Policy directive: "script-src`

<u> この問題を修正するには、次のいずれかを実行する必要があります </u>

1. `SecureHtmlRenderer` クラスを使用して、ブロックされたスクリプトを [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style) きます。
1. スクリプトの実行を許可するには、`CSPNonceProvider` クラスを使用します。
Adobe CommerceおよびMagento Open Source 2.4.7 以降には、各リクエストに一意の [!DNL nonce] 文字列を容易に生成できる **[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] プロバイダーが含まれています。 これらの [!DNL nonce] 文字列は、[!UICONTROL CSP] ヘッダーにアタッチされます。

   `Magento\Csp\Helper\CspNonceProvider` の `generateNonce` 関数を使用して、[!DNL nonce] 文字列を取得します。

   ```php
   use Magento\Csp\Helper\CspNonceProvider;
   
   class MyClass
   {
   
       /**
        * @var CspNonceProvider
        */
       private $cspNonceProvider;
   
       /**
        * @param CspNonceProvider $cspNonceProvider
        */
       public function __construct(CspNonceProvider $cspNonceProvider)
       {
           $this->cspNonceProvider = $cspNonceProvider
       }
   
       /**
        * Get CSP Nonce
        *
        * @return String
        */
       public function getNonce(): string
       {
           return $this->cspNonceProvider->generateNonce();
       }
   }
   ```

1. モジュールの `csp_whitelist.xml` ファイルに [a [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes) を追加します。

## 問題 – 支払い方法が見つからないか、機能していません

支払い方法がないか、「*インラインスクリプトの実行を拒否しました&#x200B;**が表示される**ストアフロントのチェックアウト」ページで機能しません。これは、ブラウザーコンソールログの「script-src ...*」エラーメッセージに違反しているためです。

<u> 再現手順 </u>:

1. ストアフロントに移動します。
2. 買い物かごに商品を追加し、チェックアウトに進みます。
3. 支払方法を選択します。

<u> 期待される結果 </u>:

お支払い方法を選択し、正常に注文に進むことができます。

<u> 実際の結果 </u>:

支払い方法がないか、機能していません。 「*コンテンツセキュリティポリシーディレクティブ「script-src ...*」に違反しているので、インラインスクリプトの実行を拒否しました」という [!DNL JS] エラーがブラウザーコンソールログに表示されます

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、**[!UICONTROL CSP]** は、デフォルトで、ストアフロントおよび管理領域の支払いページ用に `restrict-mode` で設定され、その他のすべてのページ用に `report-only` モードで設定されます。
対応する **[!UICONTROL CSP]** ヘッダーには、支払いページの `script-src` ディレクティブ内に `unsafe-inline` キーワードが含まれていません。 また、[!DNL whitelisted] インラインスクリプトのみ使用できます。

### 解決策

次の理由で特定のスクリプトがブロックされると、ブラウザーエラーが表示される場合が **[!UICONTROL CSP]** ります。

`Refused to execute inline script because it violates the following Content Security Policy directive: "script-src`

<u> この問題を修正するには、次のいずれかを実行する必要があります </u>

1. `SecureHtmlRenderer` クラスを使用して、ブロックされたスクリプトを [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style) きます。
1. スクリプトの実行を許可するには、`CSPNonceProvider` クラスを使用します。
Adobe CommerceおよびMagento Open Source 2.4.7 以降には、各リクエストに一意の [!DNL nonce] 文字列を容易に生成できる **[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] プロバイダーが含まれています。 これらの [!DNL nonce] 文字列は、[!UICONTROL CSP] ヘッダーにアタッチされます。

   `Magento\Csp\Helper\CspNonceProvider` の `generateNonce` 関数を使用して、[!DNL nonce] 文字列を取得します。

   ```php
   use Magento\Csp\Helper\CspNonceProvider;
   
   class MyClass
   {
   
       /**
        * @var CspNonceProvider
        */
       private $cspNonceProvider;
   
       /**
        * @param CspNonceProvider $cspNonceProvider
        */
       public function __construct(CspNonceProvider $cspNonceProvider)
       {
           $this->cspNonceProvider = $cspNonceProvider
       }
   
       /**
        * Get CSP Nonce
        *
        * @return String
        */
       public function getNonce(): string
       {
           return $this->cspNonceProvider->generateNonce();
       }
   }
   ```

1. モジュールの `csp_whitelist.xml` ファイルに [a [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes) を追加します。

## 問題 – 顧客が注文できない

顧客は、ブラウザーコンソールログのコンテンツセキュリティポリシーディレクティブ「script-src ...*」に違反するので、「* インラインスクリプトの実行を拒否されました」というエラーメッセージで注文できません。

<u> 再現手順 </u>:

1. ストアフロントに移動します。
2. 買い物かごに商品を追加し、チェックアウトに進みます。
3. 支払方法を選択します。
4. **Place Order** をクリックします。

<u> 期待される結果 </u>:

注文は正常に行われます。

<u> 実際の結果 </u>:

注文することはできません。 「*コンテンツセキュリティポリシーディレクティブ「script-src ...*」に違反しているので、インラインスクリプトの実行を拒否しました」という [!DNL JS] エラーがブラウザーコンソールログに表示されます

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、**[!UICONTROL CSP]** は、デフォルトで、ストアフロントおよび管理領域の支払いページ用に `restrict-mode` で設定され、その他のすべてのページ用に `report-only` モードで設定されます。
対応する **[!UICONTROL CSP]** ヘッダーには、支払いページの `script-src` ディレクティブ内に `unsafe-inline` キーワードが含まれていません。 また、[!DNL whitelisted] インラインスクリプトのみ使用できます。

### 解決策

次の理由で特定のスクリプトがブロックされると、ブラウザーエラーが表示される場合が **[!UICONTROL CSP]** ります。

`Refused to execute inline script because it violates the following Content Security Policy directive: "script-src`

<u> この問題を修正するには、次のいずれかを実行する必要があります </u>

1. `SecureHtmlRenderer` クラスを使用して、ブロックされたスクリプトを [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style) きます。
1. スクリプトの実行を許可するには、`CSPNonceProvider` クラスを使用します。
Adobe CommerceおよびMagento Open Source 2.4.7 以降には、各リクエストに一意の [!DNL nonce] 文字列を容易に生成できる **[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] プロバイダーが含まれています。 これらの [!DNL nonce] 文字列は、[!UICONTROL CSP] ヘッダーにアタッチされます。

   `Magento\Csp\Helper\CspNonceProvider` の `generateNonce` 関数を使用して、[!DNL nonce] 文字列を取得します。

   ```php
   use Magento\Csp\Helper\CspNonceProvider;
   
   class MyClass
   {
   
       /**
        * @var CspNonceProvider
        */
       private $cspNonceProvider;
   
       /**
        * @param CspNonceProvider $cspNonceProvider
        */
       public function __construct(CspNonceProvider $cspNonceProvider)
       {
           $this->cspNonceProvider = $cspNonceProvider
       }
   
       /**
        * Get CSP Nonce
        *
        * @return String
        */
       public function getNonce(): string
       {
           return $this->cspNonceProvider->generateNonce();
       }
   }
   ```

1. モジュールの `csp_whitelist.xml` ファイルに [a [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes) を追加します。
