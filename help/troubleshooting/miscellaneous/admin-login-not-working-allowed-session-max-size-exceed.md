---
title: '[!UICONTROL Admin] ログインが機能しません – セッションの最大サイズを超えています'
description: '[!UICONTROL Admin] パネルにログインしようとしたときにフォームが更新され、ログインできない場合の問題を解決します。'
exl-id: 12789df0-6130-4e60-a92a-68ed329bd7fd
source-git-commit: fe4a48581bdfe24da5082b69fb26a8032bd77334
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# [!UICONTROL Admin] ログインが機能しません – セッションの最大サイズを超えています

この記事では、[!UICONTROL Admin] パネルにログインしようとしたが、フォームが更新されただけでログインできない場合、または[!UICONTROL Admin] パネルで一部のアクションを実行して自動的にログアウトする場合の修正について説明します。
これは、[!UICONTROL Admin] [!UICONTROL Session Size]を超えたことが原因です。

## 影響のあるバージョン

* Adobe Commerce オンプレミス、[ サポートされているすべてのバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)
* クラウドインフラストラクチャ上のAdobe Commerce、[ サポートされているすべてのバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## イシュー

[!UICONTROL Admin]で次のいずれかの現象が発生します。

1. フォームが再読み込みを続けているため、[!UICONTROL Admin]にログインできません。
1. アクションを実行しようとすると、自動的にログアウトされます。

## 原因

許可されているセッションの最大サイズを超えています。

## Solution

次のようなエラーがないか、`var/log/support_report.log` ファイルを確認します。

*[2023-07-13T04:26:09.792060+00:00] report.WARNING: 260572のセッション サイズが、許可されているセッションの最大サイズである256000を超えています。[] []
[2023-07-13T04:26:17.056714+00:00] report.WARNING: 260570のセッション サイズが、許可されているセッションの最大サイズである256000を超えています。[][]*

これらのエラーが表示された場合、解決策は次のようになります。

<u>Adobe Commerce オンプレミス </u>:
1. バックエンド設定から&#x200B;**[!UICONTROL Max Session Size in Admin]**&#x200B;値を増やします。 これを行うには、**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Security]** > **[!UICONTROL Max Session Size in Admin]**&#x200B;に移動します。
1. 値を&#x200B;*500000*&#x200B;以上に設定します。 エラーで報告された既存の最大サイズに応じて、値を&#x200B;*0*&#x200B;に設定して、セッションサイズの制限を削除することもできます。

<u> クラウドインフラストラクチャ上のAdobe Commerce</u>:

（この設定は、デプロイメント/操作モードが&#x200B;*デフォルト*&#x200B;または&#x200B;*開発者*&#x200B;の[!UICONTROL Admin]でのみアクセスできます。 ただし、クラウド環境では実稼動デプロイメントモードのみが許可されます）。

この値を増やすには、ターミナル（SSH）で次のコマンドを実行します。

```ssh
bin/magento config:set system/security/max_session_size_admin 500000
```

エラーで報告された既存の最大サイズに応じて、*500000*&#x200B;より大きく設定できます。また、値を&#x200B;*0*&#x200B;に設定して、セッションサイズの制限を削除することもできます。

## 関連トピックス

* 管理者システムガイドの[ セッションサイズ ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-session-management#admin-sessions)
* 設定ガイドの[操作モード ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/set-mode)
* Commerce on Cloud Infrastructure ガイドの[ セキュアな接続](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections)
