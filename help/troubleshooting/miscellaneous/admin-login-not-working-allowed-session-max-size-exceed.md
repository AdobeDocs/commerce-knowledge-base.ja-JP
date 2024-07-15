---
title: 「[!DNL Admin] ログインが機能していません – 許可されているセッションの最大サイズを超えています」
description: パネルにログインしようとすると、フォームが更新され  [!DNL Admin]  ログインできない場合は、問題を解決してください。
exl-id: 12789df0-6130-4e60-a92a-68ed329bd7fd
source-git-commit: 8718148f6d9a40c9a71484a7fbc818a626e825e1
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# [!DNL Admin] ログインが動作していません – 許可されているセッションの最大サイズを超えています

この記事では、[!DNL Admin] パネルにログインしようとしてフォームが更新され、ログインできない場合の対処方法を説明します。 これは、[!DNL Admin] セッションサイズを超えていることが原因です。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス、[ サポートされているすべてのバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)
* クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 問題

フォームは再読み込みを続けるので、[!DNL Admin] にログインすることはできません。

## 原因：

許可されているセッションの最大サイズを超えています。

## 解決策

`var/log/support_report.log` ファイルで、次のようなエラーを確認します。

*[2023-07-13T04:26:09.792060+00:00] report.WARNING: 260572 のセッションサイズが、許可されているセッションの最大サイズである 256000 を超えています。 [] []
[2023-07-13T04:26:17.056714+00:00] report.WARNING: 260570 のセッションサイズが、許可されているセッションの最大サイズ 256000 を超えています。[][]*

これらのエラーが表示された場合、解決策は次のようになります。

<u>Adobe Commerce オンプレミス </u>:
1. バックエンド設定から **[!UICONTROL Max Session Size in Admin]** 値を増やします。 これを行うには、**[!UICONTROL Stores]**/**[!UICONTROL Settings]**/**[!UICONTROL Configuration]**/**[!UICONTROL Advanced]**/**[!UICONTROL System]**/**[!UICONTROL Security]**/**[!UICONTROL Max Session Size in Admin]** に移動します。
1. 値を *500000* 以上に設定します。 エラーで報告された既存の最大サイズに応じて、値を *0 に設定することもできます。これにより* セッションサイズの制限が削除されます。

<u> クラウドインフラストラクチャー上のAdobe Commerce</u>:

（この設定は、デプロイメント/操作モードがデフォルトまたは開発者の場合にのみ、[!DNL Admin] でアクセスできます。 ただし、クラウド環境で使用できるのは、実稼動デプロイメントモードのみです。）

この値を増やすには、ターミナル（SSH）で次のコマンドを実行します。

```ssh
bin/magento config:set system/security/max_session_size_admin 500000
```

エラーで報告された既存の最大サイズに応じて、*500000* より大きい値を設定したり、値を *0* に設定してセッションサイズの制限を削除したりできます。

## 関連資料

* 「管理システムガイド」の [ セッションサイズ ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-session-management#admin-sessions)。
* 設定ガイドの [ 操作モード ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/set-mode)。
* Commerce on Cloud Infrastructure ガイドの [ 安全な接続 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections)。
