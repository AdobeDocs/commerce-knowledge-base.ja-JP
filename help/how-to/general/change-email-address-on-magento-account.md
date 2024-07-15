---
title: フィールドがグレー表示されている場合に、magento.com アカウントのメールアドレスを変更する方法
description: この記事では、フィールドがグレー表示されている場合に [Magento.com] （https://account.magento.com） アカウントのメールアドレスを変更する方法について説明します。
exl-id: cd527203-345c-4318-8ca8-0063109b5f79
feature: Communications
source-git-commit: 83b21845cd306336e1cb193a9541478c8a38eea8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# フィールドがグレー表示されている場合に、magento.com アカウントのメールアドレスを変更する方法

この記事では、フィールドがグレー表示されている場合に、[Magento.com](https://account.magento.com) アカウントのメールアドレスを変更する方法について説明します。

## 影響を受ける製品とバージョン

* すべてのAdobe Commerceのバージョンとインフラストラクチャタイプ

## 原因：

[Magento.com](https://account.magento.com) アカウントの電子メール アドレスは、<https://account.adobe.com> でAdobeアカウントにリンクされており、そこで更新する必要があります。

## メールアドレスを変更する手順

### ケース I:

<https://account.adobe.com> に独自のアカウントを持つユーザーの電子メールアドレスの変更

<u> 解決策 </u>

1. 次の内容を記載したメールをGrp-magento-HelpCenterLoginIssues@adobe.comに送信します。

   * 更新する既存のメールアドレス
   * 新しいメールアドレス
   * 新しいアカウントの画像 ID （使用可能な場合）

1. 既存のアカウントのメールアドレスを更新するには、両方のアカウントを結合するようにチームにリクエストします。

### ケース II:

現在 <https://account.adobe.com> に独自のアカウントを持っていないユーザーの E メール アドレスを変更しています

<u> 解決策 </u>

[ 現在の所有者の電子メール ] のメールボックスにアクセスできる場合は、Creative Cloud ユーザーガイドの [ パスワードのリセットまたはパスワードの変更 ](https://helpx.adobe.com/manage-account/using/change-or-reset-password.html) ガイドに従って、現在の所有者の電子メールのAdobeをリセットしてください。

1. 現在の所有者のメールボックスに送信されたパスワードのリセット リンクを、手順と共に見つけます。
1. 新しいパスワードを設定し、メールを [ 新規所有者のメール ] に変更します。
1. [IMS アカウント ](https://account.adobe.com/) に移動して新しいメールでログインし、パスワードを変更します。
1. メールアドレスとパスワードを変更した後、[owner.com](https://account.magento.com) に移動し、「新しいMagentoのメール [ を使用してログインし ] す。

ただし、[ 現在の所有者のメール ] に送信されたメールへのアクセス権がない場合は、次の手順に従います。

1. 会社のメールサーバー設定を使用して、[ 現在の所有者のメール ] から新しいメールへのメール転送を設定します。
1. ここで、前の手順に進みます。

## 関連資料

Creative Cloudユーザーガイドの「[ パスワードを忘れた場合のリセット ](https://helpx.adobe.com/manage-account/using/change-or-reset-password.html)」を参照してください。
