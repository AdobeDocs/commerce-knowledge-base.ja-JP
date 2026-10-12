---
title: '[!UICONTROL CSP]制限モードでの注文ページの作成のトラブルシューティング'
description: この記事では、CSP制限モードが有効になっている場合に管理者側で注文を作成する際のエラーについて説明し、これらのエラーを修正するためのソリューションを提供します。
feature: Checkout,Security,Orders,Payments
role: Developer
exl-id: c1a0886a-df1f-418a-9e4d-562b28a0d8b3
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%
---
# [!UICONTROL CSP]制限モードでの注文ページの作成のトラブルシューティング

この記事では、「*インラインスクリプトの実行を拒否しました。これは、次のContent Security Policy ディレクティブに違反するためです。「script-src ...*」。**[!UICONTROL CSP restricted mode]**&#x200B;が&#x200B;*有効*&#x200B;である管理者側での注文を作成する際のAdobe Commerce 2.4.7の問題に関する説明と修正を提供します。 ブラウザーコンソールのログにエラーメッセージが表示されます。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure、Adobe Commerce on-premises、Magento Open Source:

* 2.4.7
* 2.4.6-pX
* 2.4.5-pX
* 2.4.4-pX

## 問題 – 管理者&#x200B;**注文作成** ページが壊れているか、読み込めません

管理者&#x200B;**作成注文** ページが壊れているか、読み込めません。次のコンテンツセキュリティポリシーディレクティブに違反しているため、「*インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot; ブラウザーコンソールのログにエラーメッセージが表示されます。

<u>複製する手順</u>:

1. **[!UICONTROL Sales]** > **[!UICONTROL Orders]**&#x200B;に移動します。
1. 新しい注文を作成します。

<u>期待される結果</u>:

管理者&#x200B;**注文作成** ページが正常に読み込まれます。

<u>実際の結果</u>:

管理者&#x200B;**注文作成** ページが空白であるか、コンポーネントが見つかりません。 次の[!DNL JS] エラーがブラウザーコンソールのログに表示されます。「*次のContent Security Policy ディレクティブに違反しているため、インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot;

### 原因

Adobe CommerceおよびMagento Open Source バージョン 2.4.7以降では、デフォルトで&#x200B;**[!UICONTROL CSP]**&#x200B;がストアフロントおよび管理領域の支払いページ用に`restrict-mode`、およびその他のすべてのページ用に`report-only` モードで設定されています。
対応する**[!UICONTROL CSP]** ヘッダーには、支払いページの`script-src` ディレクティブ内に`unsafe-inline` キーワードが含まれていません。 また、[!DNL whitelisted]個のインラインスクリプトのみが許可されます。

### Solution

[!UICONTROL CSP]が原因で特定のスクリプトがブロックされているため、ブラウザーのエラーが表示される場合があります。

`Refused to execute inline script because it violates the following [!UICONTROL Content Security Policy] directive: "script-src`

<u>この問題を修正するには、</u>のいずれかを実行する必要があります。

1. [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style)は、`SecureHtmlRenderer` クラスを使用してブロックされたスクリプトです。
1. スクリプトの実行を許可するには、`CSPNonceProvider` クラスを使用します。
Adobe CommerceおよびMagento Open Source 2.4.7以降には、各リクエストに対して一意の[!DNL nonce]文字列を簡単に生成できる&#x200B;**[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] プロバイダーが含まれています。 これらの[!DNL nonce]文字列は[!UICONTROL CSP] ヘッダーにアタッチされます。

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

管理者&#x200B;**注文作成ページ**&#x200B;で支払い方法が見つからないか、機能していません。次のコンテンツセキュリティポリシーに違反しているため、「*インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot; ブラウザーコンソールのログにエラーメッセージが表示されます。

<u>複製する手順</u>:

1. **[!UICONTROL Sales]** > **[!UICONTROL Orders]**&#x200B;に移動します。
1. 新しい注文を作成します。
1. 新規顧客の作成：
1. 顧客の詳細を入力します。
1. 注文の詳細（商品、配送方法）を入力します。
1. 支払い方法を選択します。

<u>期待される結果</u>:

お支払い方法を選択し、正常に注文を行うことができます。

<u>実際の結果</u>:

支払い方法がないか、機能しません。 次の[!DNL JS] エラーがブラウザーコンソールのログに表示されます。「*インラインスクリプトの実行を拒否しました。これは、次のコンテンツセキュリティポリシーディレクティブに違反しているためです。「script-src ...*」

### 原因

Adobe CommerceおよびMagento Open Source バージョン 2.4.7以降では、デフォルトで&#x200B;**[!UICONTROL CSP]**&#x200B;がストアフロントおよび管理領域の支払いページ用に`restrict-mode`、およびその他のすべてのページ用に`report-only` モードで設定されています。
対応する**[!UICONTROL CSP]** ヘッダーには、支払いページの`script-src` ディレクティブ内に`unsafe-inline` キーワードが含まれていません。 また、[!DNL whitelisted]個のインラインスクリプトのみが許可されます。

### Solution

**[!UICONTROL CSP]**&#x200B;が原因で特定のスクリプトがブロックされているため、ブラウザーのエラーが表示される場合があります。

`Refused to execute inline script because it violates the following [!UICONTROL Content Security Policy] directive: "script-src`

<u>この問題を修正するには、</u>のいずれかを実行する必要があります。

1. [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style)は、`SecureHtmlRenderer` クラスを使用してブロックされたスクリプトです。
1. スクリプトの実行を許可するには、`CSPNonceProvider` クラスを使用します。
Adobe CommerceおよびMagento Open Source 2.4.7以降には、各リクエストに対して一意の[!DNL nonce]文字列を簡単に生成できる&#x200B;**[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] プロバイダーが含まれています。 これらの[!DNL nonce]文字列は[!UICONTROL CSP] ヘッダーにアタッチされます。

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

1. モジュールの`csp_whitelist.xml` ファイルに[a [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes)を追加します。

## 問題 – 管理者が注文できません

管理者は、次のコンテンツセキュリティポリシーディレクティブに違反しているため、「*インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot;」を含む注文ページを作成&#x200B;**して注文を送信することはできません**&#x200B;ブラウザーコンソールのログにエラーメッセージが表示されます。

<u>複製する手順</u>:

1. **[!UICONTROL Sales]** > **[!UICONTROL Orders]**&#x200B;に移動します。
1. 新しい注文を作成します。
1. 新規顧客の作成：
1. 顧客の詳細を入力します。
1. 注文の詳細（商品、配送方法）を入力します。
1. 支払い方法を選択します。
1. 注文を送信します。

<u>期待される結果</u>:

注文を正常に送信できます。

<u>実際の結果</u>:

注文を送信できません。 次の[!DNL JS] エラーがブラウザーコンソールのログに表示されます。「*次のContent Security Policy ディレクティブに違反しているため、インラインスクリプトの実行を拒否しました：&quot;script-src ...*&quot;

### 原因

Adobe CommerceおよびMagento Open Source バージョン 2.4.7以降では、デフォルトで&#x200B;**[!UICONTROL CSP]**&#x200B;がストアフロントおよび管理領域の支払いページ用に`restrict-mode`、およびその他のすべてのページ用に`report-only` モードで設定されています。
対応する**[!UICONTROL CSP]** ヘッダーには、支払いページの`script-src` ディレクティブ内に`unsafe-inline` キーワードが含まれていません。 また、[!DNL whitelisted]個のインラインスクリプトのみが許可されます。

### Solution

**[!UICONTROL CSP]**&#x200B;が原因で特定のスクリプトがブロックされているため、ブラウザーのエラーが表示される場合があります。

`Refused to execute inline script because it violates the following [!UICONTROL Content Security Policy] directive: "script-src`

<u>この問題を修正するには、</u>のいずれかを実行する必要があります。

1. [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style)は、`SecureHtmlRenderer` クラスを使用してブロックされたスクリプトです。
1. スクリプトの実行を許可するには、`CSPNonceProvider` クラスを使用します。
Adobe CommerceおよびMagento Open Source 2.4.7以降には、各リクエストに対して一意の[!DNL nonce]文字列を簡単に生成できる&#x200B;**[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] プロバイダーが含まれています。 これらの[!DNL nonce]文字列は[!UICONTROL CSP] ヘッダーにアタッチされます。

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
