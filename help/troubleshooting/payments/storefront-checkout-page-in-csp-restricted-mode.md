---
title: のストアフロントのチェックアウトページのトラブルシューティング [!UICONTROL CSP] 制限付きモード
description: この記事では、CSP 制限モードでチェックアウトページを表示している際に発生する可能性のあるエラーについて説明し、それらのエラーを修正するソリューションを提供します。
feature: Checkout,Security,Orders,Payments
role: Developer
exl-id: fb92b75d-c88b-4810-a309-d6ab38485e86
source-git-commit: 6d0c4ea9576440d66be3b8053a6e362b8ac0ebcb
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# のストアフロントのチェックアウトページのトラブルシューティング [!UICONTROL CSP] 制限付きモード

ここでは、でチェックアウトページを表示する際のAdobe Commerce 2.4.7 の問題に関する説明と修正点を説明します。 **[!UICONTROL CSP restricted mode]**、「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*&#x200B;ブラウザーコンソールログに「エラーメッセージ。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure、Adobe Commerce オンプレミス、およびMagento Open Source:

* 2.4.7
* 2.4.6-pX
* 2.4.5-pX
* 2.4.4-pX

## 問題 – ストアフロントのチェックアウトページが壊れているか、読み込めません

この **ストアフロントのチェックアウト** 「」により、ページが壊れているか、読み込めません&#x200B;*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*&#x200B;ブラウザーコンソールログに「エラーメッセージ。

<u>再現手順</u>:

1. ストアフロントに移動します。
1. 買い物かごに商品を追加し、チェックアウトに進みます。

<u>期待される結果</u>:

チェックアウトページが正常に読み込まれる。

<u>実際の結果</u>:

チェックアウトページが空白であるか、コンポーネントがありません。 次の [!DNL JS] 次のエラーがブラウザーコンソールログに表示されます。「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*“

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、 **[!UICONTROL CSP]** はで設定されています `restrict-mode`デフォルトでは、ストアフロントおよび管理領域およびの支払いページ用 `report-only` その他すべてのページのモード。
対応する **[!UICONTROL CSP]** ヘッダーにが含まれていない `unsafe-inline` 内のキーワード `script-src` 支払いページのディレクティブ。 また、のみ [!DNL whitelisted] インラインスクリプトを使用できます。

### 解決策

特定のスクリプトが次の理由でブロックされることで、ブラウザーエラーが発生する場合があります。 **[!UICONTROL CSP]**:

`Refused to execute inline script because it violates the following Content Security Policy directive: "script-src`

<u>この問題を修正するには、次のいずれかを実行する必要があります</u>:

1. [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style) を使用してブロックされたスクリプト `SecureHtmlRenderer` クラス。
1. の使用 `CSPNonceProvider` スクリプトの実行を許可するクラス。
Adobe CommerceおよびMagento Open Source 2.4.7 以降には、 **[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] 一意のの生成を容易にするプロバイダー [!DNL nonce] 各リクエストの文字列。 これら [!DNL nonce] 次に、文字列がに添付されます [!UICONTROL CSP] ヘッダー。

   の使用 `generateNonce` 関数 `Magento\Csp\Helper\CspNonceProvider` 手に入れる [!DNL nonce] 文字列。

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

1. [を追加 [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes) モジュールのに `csp_whitelist.xml` ファイル。

## 問題 – 支払い方法が見つからないか、機能していません

支払い方法がないか、で機能していません **ストアフロントのチェックアウト** ページ （「」付き）*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*&#x200B;ブラウザーコンソールログに「エラーメッセージ。

<u>再現手順</u>:

1. ストアフロントに移動します。
2. 買い物かごに商品を追加し、チェックアウトに進みます。
3. 支払方法を選択します。

<u>期待される結果</u>:

お支払い方法を選択し、正常に注文に進むことができます。

<u>実際の結果</u>:

支払い方法がないか、機能していません。 次の [!DNL JS] 次のエラーがブラウザーコンソールログに表示されます。「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*“

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、 **[!UICONTROL CSP]** はで設定されています `restrict-mode`デフォルトでは、ストアフロントおよび管理領域およびの支払いページ用 `report-only` その他すべてのページのモード。
対応する **[!UICONTROL CSP]** ヘッダーにが含まれていない `unsafe-inline` 内のキーワード `script-src` 支払いページのディレクティブ。 また、のみ [!DNL whitelisted] インラインスクリプトを使用できます。

### 解決策

特定のスクリプトが次の理由でブロックされることで、ブラウザーエラーが発生する場合があります。 **[!UICONTROL CSP]**:

`Refused to execute inline script because it violates the following Content Security Policy directive: "script-src`

<u>この問題を修正するには、次のいずれかを実行する必要があります</u>:

1. [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style) を使用してブロックされたスクリプト `SecureHtmlRenderer` クラス。
1. の使用 `CSPNonceProvider` スクリプトの実行を許可するクラス。
Adobe CommerceおよびMagento Open Source 2.4.7 以降には、 **[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] 一意のの生成を容易にするプロバイダー [!DNL nonce] 各リクエストの文字列。 これら [!DNL nonce] 次に、文字列がに添付されます [!UICONTROL CSP] ヘッダー。

   の使用 `generateNonce` 関数 `Magento\Csp\Helper\CspNonceProvider` 手に入れる [!DNL nonce] 文字列。

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

1. [を追加 [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes) モジュールのに `csp_whitelist.xml` ファイル。

## 問題 – 顧客が注文できない

顧客は「」を使用して注文することはできません&#x200B;*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*&#x200B;ブラウザーコンソールログに「エラーメッセージ。

<u>再現手順</u>:

1. ストアフロントに移動します。
2. 買い物かごに商品を追加し、チェックアウトに進みます。
3. 支払方法を選択します。
4. クリック **注文する**.

<u>期待される結果</u>:

注文は正常に行われます。

<u>実際の結果</u>:

注文することはできません。 次の [!DNL JS] 次のエラーがブラウザーコンソールログに表示されます。「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*“

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、 **[!UICONTROL CSP]** はで設定されています `restrict-mode`デフォルトでは、ストアフロントおよび管理領域およびの支払いページ用 `report-only` その他すべてのページのモード。
対応する **[!UICONTROL CSP]** ヘッダーにが含まれていない `unsafe-inline` 内のキーワード `script-src` 支払いページのディレクティブ。 また、のみ [!DNL whitelisted] インラインスクリプトを使用できます。

### 解決策

特定のスクリプトが次の理由でブロックされることで、ブラウザーエラーが発生する場合があります。 **[!UICONTROL CSP]**:

`Refused to execute inline script because it violates the following Content Security Policy directive: "script-src`

<u>この問題を修正するには、次のいずれかを実行する必要があります</u>:

1. [[!DNL Whitelist]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#whitelist-an-inline-script-or-style) を使用してブロックされたスクリプト `SecureHtmlRenderer` クラス。
1. の使用 `CSPNonceProvider` スクリプトの実行を許可するクラス。
Adobe CommerceおよびMagento Open Source 2.4.7 以降には、 **[!UICONTROL Content Security Policy (CSP)]** [!DNL nonce] 一意のの生成を容易にするプロバイダー [!DNL nonce] 各リクエストの文字列。 これら [!DNL nonce] 次に、文字列がに添付されます [!UICONTROL CSP] ヘッダー。

   の使用 `generateNonce` 関数 `Magento\Csp\Helper\CspNonceProvider` 手に入れる [!DNL nonce] 文字列。

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

1. [を追加 [!DNL hash]](https://developer.adobe.com/commerce/php/development/security/content-security-policies/#using-inline-scripts-and-styles-is-discouraged-in-favor-of-ui-components-and-classes) モジュールのに `csp_whitelist.xml` ファイル。
