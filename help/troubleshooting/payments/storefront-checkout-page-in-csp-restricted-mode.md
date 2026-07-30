---
title: '[!UICONTROL CSP]制限モードでのストアフロントチェックアウトページのトラブルシューティング'
description: この記事では、CSP制限モードでチェックアウトページを表示する際に発生する可能性のあるエラーについて説明し、これらのエラーを修正するためのソリューションを提供します。
feature: Checkout,Security,Orders,Payments
role: Developer
exl-id: fb92b75d-c88b-4810-a309-d6ab38485e86
source-git-commit: 6d0c4ea9576440d66be3b8053a6e362b8ac0ebcb
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 0%

---

# [!UICONTROL CSP]制限モードでのストアフロントチェックアウトページのトラブルシューティング

この記事では、次のContent Security Policy ディレクティブに違反しているため、「*インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot;」を使用して、**[!UICONTROL CSP restricted mode]**&#x200B;のチェックアウトページを表示する際のAdobe Commerce 2.4.7の問題に関する説明と修正について説明します。 ブラウザーコンソールのログにエラーメッセージが表示されます。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure、Adobe Commerce on-premises、Magento Open Source:

* 2.4.7
* 2.4.6-pX
* 2.4.5-pX
* 2.4.4-pX

## 問題 – ストアフロントのチェックアウトページが壊れているか、読み込めません

**ストアフロント チェックアウト** ページが壊れているか読み込めません。次のContent Security Policy ディレクティブに違反しているため、「*インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot; ブラウザーコンソールのログにエラーメッセージが表示されます。

<u>複製する手順</u>:

1. ストアフロントに移動します。
1. 商品をカートに追加し、チェックアウトに進みます。

<u>期待される結果</u>:

チェックアウトページは正常に読み込まれます。

<u>実際の結果</u>:

チェックアウトページが空白であるか、コンポーネントが欠落しています。 次の[!DNL JS] エラーがブラウザーコンソールのログに表示されます。「*次のContent Security Policy ディレクティブに違反しているため、インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot;

### 原因

Adobe CommerceおよびMagento Open Source バージョン 2.4.7以降では、デフォルトで&#x200B;**[!UICONTROL CSP]**&#x200B;がストアフロントおよび管理領域の支払いページ用に`restrict-mode`、およびその他のすべてのページ用に`report-only` モードで設定されています。
対応する**[!UICONTROL CSP]** ヘッダーには、支払いページの`script-src` ディレクティブ内に`unsafe-inline` キーワードが含まれていません。また、[!DNL whitelisted]個のインラインスクリプトのみが許可されます。

### Solution

**[!UICONTROL CSP]**&#x200B;が原因で特定のスクリプトがブロックされているため、ブラウザーのエラーが表示される場合があります。

`Refused to execute inline script because it violates the following Content Security Policy directive: "script-src`

<u>この問題を修正するには、</u>のいずれかを実行する必要があります。

1. [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style)は、`SecureHtmlRenderer` クラスを使用してブロックされたスクリプトです。
1. スクリプトの実行を許可するには、`CSPNonceProvider` クラスを使用します。
Adobe CommerceおよびMagento Open Source 2.4.7以降には、各リクエストに対して一意の[!DNL nonce]文字列を簡単に生成できる&#x200B;**[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] プロバイダーが含まれています。次に、これらの[!DNL nonce]文字列が[!UICONTROL CSP] ヘッダーにアタッチされます。

   `Magento\Csp\Helper\CspNonceProvider`の`generateNonce`関数を使用して、[!DNL nonce]文字列を取得します。

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

1. [ モジュールの`csp_whitelist.xml` ファイルに [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes)を追加します。

## 問題 – 支払い方法がないか、機能しません

支払い方法が見つからないか、**storefront チェックアウト** ページで機能していません。また、「*インラインスクリプトの実行を拒否しました。これは、次のコンテンツセキュリティポリシーディレクティブに違反しているためです。「script-src ...*」 ブラウザーコンソールのログにエラーメッセージが表示されます。

<u>複製する手順</u>:

1. ストアフロントに移動します。
2. 商品をカートに追加し、チェックアウトに進みます。
3. 支払い方法を選択します。

<u>期待される結果</u>:

お支払い方法を選択し、正常に注文を行うことができます。

<u>実際の結果</u>:

支払い方法がないか、機能しません。 次の[!DNL JS] エラーがブラウザーコンソールのログに表示されます。「*次のContent Security Policy ディレクティブに違反しているため、インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot;

### 原因

Adobe CommerceおよびMagento Open Source バージョン 2.4.7以降では、デフォルトで&#x200B;**[!UICONTROL CSP]**&#x200B;がストアフロントおよび管理領域の支払いページ用に`restrict-mode`、およびその他のすべてのページ用に`report-only` モードで設定されています。
対応する**[!UICONTROL CSP]** ヘッダーには、支払いページの`script-src` ディレクティブ内に`unsafe-inline` キーワードが含まれていません。また、[!DNL whitelisted]個のインラインスクリプトのみが許可されます。

### Solution

**[!UICONTROL CSP]**&#x200B;が原因で特定のスクリプトがブロックされているため、ブラウザーのエラーが表示される場合があります。

`Refused to execute inline script because it violates the following Content Security Policy directive: "script-src`

<u>この問題を修正するには、</u>のいずれかを実行する必要があります。

1. [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style)は、`SecureHtmlRenderer` クラスを使用してブロックされたスクリプトです。
1. スクリプトの実行を許可するには、`CSPNonceProvider` クラスを使用します。
Adobe CommerceおよびMagento Open Source 2.4.7以降には、各リクエストに対して一意の[!DNL nonce]文字列を簡単に生成できる&#x200B;**[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] プロバイダーが含まれています。次に、これらの[!DNL nonce]文字列が[!UICONTROL CSP] ヘッダーにアタッチされます。

   `Magento\Csp\Helper\CspNonceProvider`の`generateNonce`関数を使用して、[!DNL nonce]文字列を取得します。

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

1. [ モジュールの`csp_whitelist.xml` ファイルに [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes)を追加します。

## 問題 – お客様が注文できません

「*インラインスクリプトの実行を拒否しました。これは、次のコンテンツセキュリティポリシーディレクティブに違反しているためです。「script-src ...*」 ブラウザーコンソールのログにエラーメッセージが表示されます。

<u>複製する手順</u>:

1. ストアフロントに移動します。
2. 商品をカートに追加し、チェックアウトに進みます。
3. 支払い方法を選択します。
4. 「**注文を配置**」をクリックします。

<u>期待される結果</u>:

正常に注文できるようになりました。

<u>実際の結果</u>:

注文はできません。 次の[!DNL JS] エラーがブラウザーコンソールのログに表示されます。「*次のContent Security Policy ディレクティブに違反しているため、インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot;

### 原因

Adobe CommerceおよびMagento Open Source バージョン 2.4.7以降では、デフォルトで&#x200B;**[!UICONTROL CSP]**&#x200B;がストアフロントおよび管理領域の支払いページ用に`restrict-mode`、およびその他のすべてのページ用に`report-only` モードで設定されています。
対応する**[!UICONTROL CSP]** ヘッダーには、支払いページの`script-src` ディレクティブ内に`unsafe-inline` キーワードが含まれていません。また、[!DNL whitelisted]個のインラインスクリプトのみが許可されます。

### Solution

**[!UICONTROL CSP]**&#x200B;が原因で特定のスクリプトがブロックされているため、ブラウザーのエラーが表示される場合があります。

`Refused to execute inline script because it violates the following Content Security Policy directive: "script-src`

<u>この問題を修正するには、</u>のいずれかを実行する必要があります。

1. [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style)は、`SecureHtmlRenderer` クラスを使用してブロックされたスクリプトです。
1. スクリプトの実行を許可するには、`CSPNonceProvider` クラスを使用します。
Adobe CommerceおよびMagento Open Source 2.4.7以降には、各リクエストに対して一意の[!DNL nonce]文字列を簡単に生成できる&#x200B;**[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] プロバイダーが含まれています。次に、これらの[!DNL nonce]文字列が[!UICONTROL CSP] ヘッダーにアタッチされます。

   `Magento\Csp\Helper\CspNonceProvider`の`generateNonce`関数を使用して、[!DNL nonce]文字列を取得します。

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

1. [ モジュールの`csp_whitelist.xml` ファイルに [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes)を追加します。
