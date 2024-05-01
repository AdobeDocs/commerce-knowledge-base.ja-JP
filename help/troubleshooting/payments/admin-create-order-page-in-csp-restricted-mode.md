---
title: での注文ページ作成のトラブルシューティング [!UICONTROL CSP] 制限付きモード
description: この記事では、CSP 制限モードが有効な場合に管理者側で注文を作成する際に発生するエラーについて説明し、これらのエラーを修正するためのソリューションを提供します。
feature: Checkout,Security,Orders,Payments
role: Developer
exl-id: c1a0886a-df1f-418a-9e4d-562b28a0d8b3
source-git-commit: 6d0c4ea9576440d66be3b8053a6e362b8ac0ebcb
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# での注文ページ作成のトラブルシューティング [!UICONTROL CSP] 制限付きモード

ここでは、を使用して管理者側で注文を行う際のAdobe Commerce 2.4.7 の問題に関する説明と修正点を説明します **[!UICONTROL CSP restricted mode]** 等しい *Enabled*、「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*&#x200B;ブラウザーコンソールログに「エラーメッセージ。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure、Adobe Commerce オンプレミス、およびMagento Open Source:

* 2.4.7
* 2.4.6-pX
* 2.4.5-pX
* 2.4.4-pX

## 問題 – 管理者 **注文を作成** ページが壊れているか、読み込めません

管理者 **注文を作成** 「」により、ページが壊れているか、読み込めません&#x200B;*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*&#x200B;ブラウザーコンソールログに「エラーメッセージ。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. 新しい注文を作成します。

<u>期待される結果</u>:

管理者 **注文を作成** ページが正常に読み込まれます。

<u>実際の結果</u>:

管理者 **注文を作成** ページが空白か、コンポーネントがありません。 次の [!DNL JS] 次のエラーがブラウザーコンソールログに表示されます。「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*“

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、 **[!UICONTROL CSP]** はで設定されています `restrict-mode`デフォルトでは、ストアフロントおよび管理領域およびの支払いページ用 `report-only` その他すべてのページのモード。
対応する **[!UICONTROL CSP]** ヘッダーにが含まれていない `unsafe-inline` 内のキーワード `script-src` 支払いページのディレクティブ。 また、のみ [!DNL whitelisted] インラインスクリプトを使用できます。

### 解決策

特定のスクリプトが次の理由でブロックされることで、ブラウザーエラーが発生する場合があります。 [!UICONTROL CSP]:

`Refused to execute inline script because it violates the following [!UICONTROL Content Security Policy] directive: "script-src`

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

支払い方法がないか、管理者で機能していません **注文作成ページ**、「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*&#x200B;ブラウザーコンソールログに「エラーメッセージ。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. 新しい注文を作成します。
1. 顧客を新規作成します。
1. 顧客詳細を入力します。
1. 注文の詳細（製品、発送方法）を入力します。
1. 支払方法を選択します。

<u>期待される結果</u>:

お支払い方法を選択し、正常に注文に進むことができます。

<u>実際の結果</u>:

支払い方法がないか、機能していません。 次の [!DNL JS] 次のエラーがブラウザーコンソールログに表示されます。「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*」と入力します。

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、 **[!UICONTROL CSP]** はで設定されています `restrict-mode`デフォルトでは、ストアフロントおよび管理領域およびの支払いページ用 `report-only` その他すべてのページのモード。
対応する **[!UICONTROL CSP]** ヘッダーにが含まれていない `unsafe-inline` 内のキーワード `script-src` 支払いページのディレクティブ。 また、のみ [!DNL whitelisted] インラインスクリプトを使用できます。

### 解決策

特定のスクリプトが次の理由でブロックされることで、ブラウザーエラーが発生する場合があります。 **[!UICONTROL CSP]**:

`Refused to execute inline script because it violates the following [!UICONTROL Content Security Policy] directive: "script-src`

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

## 問題 – 管理者が注文できない

管理者は、管理者に注文を送信できません **注文ページを作成**、「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*&#x200B;ブラウザーコンソールログに「エラーメッセージ。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. 新しい注文を作成します。
1. 顧客を新規作成します。
1. 顧客詳細を入力します。
1. 注文の詳細（製品、発送方法）を入力します。
1. 支払方法を選択します。
1. 注文を送信します。

<u>期待される結果</u>:

注文を正常に送信できます。

<u>実際の結果</u>:

注文を送信できません。 次の [!DNL JS] 次のエラーがブラウザーコンソールログに表示されます。「*コンテンツセキュリティポリシーディレクティブ「script-src ...」に違反しているため、インラインスクリプトの実行を拒否しました。*“

### 原因：

Adobe CommerceおよびMagento Open Sourceバージョン 2.4.7 以降では、 **[!UICONTROL CSP]** はで設定されています `restrict-mode`デフォルトでは、ストアフロントおよび管理領域およびの支払いページ用 `report-only` その他すべてのページのモード。
対応する **[!UICONTROL CSP]** ヘッダーにが含まれていない `unsafe-inline` 内のキーワード `script-src` 支払いページのディレクティブ。 また、のみ [!DNL whitelisted] インラインスクリプトを使用できます。

### 解決策

特定のスクリプトが次の理由でブロックされることで、ブラウザーエラーが発生する場合があります。 **[!UICONTROL CSP]**:

`Refused to execute inline script because it violates the following [!UICONTROL Content Security Policy] directive: "script-src`

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
