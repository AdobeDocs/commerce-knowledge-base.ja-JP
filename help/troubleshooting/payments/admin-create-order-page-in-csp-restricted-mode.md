---
title: 制限モードでの注文ページの作成のトラブルシューティ [!UICONTROL CSP] グ
description: この記事では、CSP 制限モードが有効な場合に管理者側で注文を作成する際に発生するエラーについて説明し、これらのエラーを修正するためのソリューションを提供します。
feature: Checkout,Security,Orders,Payments
role: Developer
exl-id: c1a0886a-df1f-418a-9e4d-562b28a0d8b3
source-git-commit: 6d0c4ea9576440d66be3b8053a6e362b8ac0ebcb
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# 制限モードでの注文ページの作成のトラブルシューティ [!UICONTROL CSP] グ

この記事では、**[!UICONTROL CSP restricted mode]** が *有効* で、かつ「*Refused to execute inline script that it refused to been following Content Security Policy directive: &quot;script-src ...*&quot;」というエラーメッセージがブラウザーコンソールログに記録される場合に、管理者側で注文を行う際のAdobe Commerce 2.4.7 の問題について説明し、修正を示します。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure、Adobe Commerce オンプレミス、およびMagento Open Source:

* 2.4.7
* 2.4.6-pX
* 2.4.5-pX
* 2.4.4-pX

## 問題 – 管理者 **注文を作成** ページが壊れているか、読み込むことができません

管理者の **注文を作成** ページが破損しているか、読み込めません。その際、「*インラインスクリプトの実行を拒否しました：ブラウザーコンソールログに次のコンテンツセキュリティポリシーディレクティブ：「script-src ...*」エラーメッセージに違反しているためです。

<u> 再現手順 </u>:

1. **[!UICONTROL Sales]**/**[!UICONTROL Orders]** に移動します。
1. 新しい注文を作成します。

<u> 期待される結果 </u>:

管理者 **注文を作成** ページが通常どおり完全に読み込まれる。

<u> 実際の結果 </u>:

管理者 **注文を作成** ページが空白であるか、コンポーネントがありません。 「*コンテンツセキュリティポリシーディレクティブ「script-src ...*」に違反しているので、インラインスクリプトの実行を拒否しました」という [!DNL JS] エラーがブラウザーコンソールログに表示されます

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、**[!UICONTROL CSP]** は、デフォルトで、ストアフロントおよび管理領域の支払いページ用に `restrict-mode` で設定され、その他のすべてのページ用に `report-only` モードで設定されます。
対応する **[!UICONTROL CSP]** ヘッダーには、支払いページの `script-src` ディレクティブ内に `unsafe-inline` キーワードが含まれていません。 また、[!DNL whitelisted] インラインスクリプトのみ使用できます。

### 解決策

次の理由で特定のスクリプトがブロックされると、ブラウザーエラーが表示される場合が [!UICONTROL CSP] ります。

`Refused to execute inline script because it violates the following [!UICONTROL Content Security Policy] directive: "script-src`

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

支払い方法がないか、管理者 **注文作成ページ** で機能せず、「*インラインスクリプトの実行を拒否しました：ブラウザーコンソールログのコンテンツセキュリティポリシーディレクティブ「script-src ...*」エラーメッセージに違反するからです。

<u> 再現手順 </u>:

1. **[!UICONTROL Sales]**/**[!UICONTROL Orders]** に移動します。
1. 新しい注文を作成します。
1. 顧客を新規作成します。
1. 顧客詳細を入力します。
1. 注文の詳細（製品、発送方法）を入力します。
1. 支払方法を選択します。

<u> 期待される結果 </u>:

お支払い方法を選択し、正常に注文に進むことができます。

<u> 実際の結果 </u>:

支払い方法がないか、機能していません。 「*コンテンツセキュリティポリシーディレクティブ「script-src ...*」に違反しているので、インラインスクリプトの実行を拒否しました」という [!DNL JS] エラーがブラウザーコンソールログに表示されます。

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、**[!UICONTROL CSP]** は、デフォルトで、ストアフロントおよび管理領域の支払いページ用に `restrict-mode` で設定され、その他のすべてのページ用に `report-only` モードで設定されます。
対応する **[!UICONTROL CSP]** ヘッダーには、支払いページの `script-src` ディレクティブ内に `unsafe-inline` キーワードが含まれていません。 また、[!DNL whitelisted] インラインスクリプトのみ使用できます。

### 解決策

次の理由で特定のスクリプトがブロックされると、ブラウザーエラーが表示される場合が **[!UICONTROL CSP]** ります。

`Refused to execute inline script because it violates the following [!UICONTROL Content Security Policy] directive: "script-src`

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

## 問題 – 管理者が注文できない

管理者は、管理者 **注文を作成ページ** で「*インラインスクリプトの実行を拒否しました：ブラウザーコンソールログのコンテンツセキュリティポリシーディレクティブ「script-src ...*」エラーメッセージに違反するからです。

<u> 再現手順 </u>:

1. **[!UICONTROL Sales]**/**[!UICONTROL Orders]** に移動します。
1. 新しい注文を作成します。
1. 顧客を新規作成します。
1. 顧客詳細を入力します。
1. 注文の詳細（製品、発送方法）を入力します。
1. 支払方法を選択します。
1. 注文を送信します。

<u> 期待される結果 </u>:

注文を正常に送信できます。

<u> 実際の結果 </u>:

注文を送信できません。 「*コンテンツセキュリティポリシーディレクティブ「script-src ...*」に違反しているので、インラインスクリプトの実行を拒否しました」という [!DNL JS] エラーがブラウザーコンソールログに表示されます

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、**[!UICONTROL CSP]** は、デフォルトで、ストアフロントおよび管理領域の支払いページ用に `restrict-mode` で設定され、その他のすべてのページ用に `report-only` モードで設定されます。
対応する **[!UICONTROL CSP]** ヘッダーには、支払いページの `script-src` ディレクティブ内に `unsafe-inline` キーワードが含まれていません。 また、[!DNL whitelisted] インラインスクリプトのみ使用できます。

### 解決策

次の理由で特定のスクリプトがブロックされると、ブラウザーエラーが表示される場合が **[!UICONTROL CSP]** ります。

`Refused to execute inline script because it violates the following [!UICONTROL Content Security Policy] directive: "script-src`

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
