---
title: '[!DNL Admin] ログインが動作していません – 許可されているセッションの最大サイズを超えています'
description: にログインしようとすると、問題を解決できる [!DNL Admin] パネルとフォームが更新され、ログインできません。
exl-id: 12789df0-6130-4e60-a92a-68ed329bd7fd
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# [!DNL Admin] ログインが動作していません – 許可されているセッションの最大サイズを超えています

この記事では、にログインしようとする際の修正方法を説明します [!DNL Admin] パネルに表示されるが、フォームが更新されたばかりで、ログインできない。 これは、 [!DNL Admin] セッションサイズを超えています。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス、 [すべてのサポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)
* クラウドインフラストラクチャー上のAdobe Commerce [すべてのサポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 問題

にログインすることはできません [!DNL Admin]フォームが再読み込みを続けるので。

## 原因：

許可されているセッションの最大サイズを超えています。

## 解決策

を確認します `var/log/support_report.log` 次のようなエラーのファイル。

*[2023-07-13T04:26:09.792060+00:00] report.WARNING: セッション サイズ 260572 は、許可されているセッションの最大サイズ 256000 を超えています。 [] []
[2023-07-13T04:26:17.056714+00:00] report.WARNING: セッション サイズ 260570 は、許可されているセッションの最大サイズ 256000 を超えています。 [][]*

これらのエラーが表示された場合、解決策は次のようになります。

<u>Adobe Commerce オンプレミス</u>:
1. を増やす **[!UICONTROL Max Session Size in Admin]** バックエンド設定の値。 これを行うには、に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Security]** > **[!UICONTROL Max Session Size in Admin]**.
1. 値をに設定します *500000* 以上。 エラーで報告される既存の最大サイズに応じて、の値をに設定することもできます。 *0* これにより、セッションサイズの制限が削除されます。

<u>クラウドインフラストラクチャー上のAdobe Commerce</u>:

（この設定は、 [!DNL Admin] デプロイメント/操作モードがデフォルトまたは開発者の場合。 ただし、クラウド環境で使用できるのは、実稼動デプロイメントモードのみです。）

この値を増やすには、ターミナル（SSH）で次のコマンドを実行します。

```ssh
bin/magento config:set system/security/max_session_size_admin 500000
```

を次より大きい値に設定できます *500000* エラーで報告される既存の最大サイズに応じて、の値をに設定することもできます。 *0* セッションサイズの上限を削除するには、をクリックします。

## 関連資料

* [セッションサイズ](/docs/commerce-admin/systems/security/security-session-management.html?lang=en#admin-sessions) （管理システムガイド）。
* [操作モード](/docs/commerce-operations/configuration-guide/cli/set-mode.html) （設定ガイド）を参照してください。
* [安全な接続](/docs/commerce-cloud-service/user-guide/develop/secure-connections.html) （Commerce on Cloud Infrastructure ガイド）を参照してください。
