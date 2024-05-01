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

この記事では、のメールアドレスを変更する方法を説明します [Magento.com](https://account.magento.com) フィールドがグレー表示されている場合のアカウント。

## 影響を受ける製品とバージョン

* すべてのAdobe Commerceのバージョンとインフラストラクチャタイプ

## 原因：

のメールアドレス [Magento.com](https://account.magento.com) アカウントはAdobeアカウントにリンクされています： <https://account.adobe.com> およびを更新する必要があります。

## メールアドレスを変更する手順

### ケース I:

で独自のアカウントを持つユーザーの電子メールアドレスの変更 <https://account.adobe.com>

<u>解決策</u>

1. 次の内容を記載したメールをGrp-magento-HelpCenterLoginIssues@adobe.comに送信します。

   * 更新する既存のメールアドレス
   * 新しいメールアドレス
   * 新しいアカウントの画像 ID （使用可能な場合）

1. 既存のアカウントのメールアドレスを更新するには、両方のアカウントを結合するようにチームにリクエストします。

### ケース II:

現在で独自のアカウントを持っていないユーザーのメールアドレスを変更しています <https://account.adobe.com>

<u>解決策</u>

のメールボックスにアクセスできる場合 [現在の所有者メール]、次の手順で現在の所有者の E メールのパスワードをリセットします [Adobeのパスワードをリセットまたは変更する](https://helpx.adobe.com/manage-account/using/change-or-reset-password.html) Creative Cloudユーザーガイドのガイド。

1. 現在の所有者のメールボックスに送信されたパスワードのリセット リンクを、手順と共に見つけます。
1. 新しいパスワードを設定し、メールをに変更します [新規所有者のメール].
1. に移動します。 [IMS アカウント](https://account.adobe.com/) 新しいメールでログインし、パスワードを変更します。
1. メールアドレスとパスワードを変更したら、に移動します。 [Magento.com](https://account.magento.com) を使用してログインするには [新規所有者のメール].

ただし、に送信されるメールへのアクセス権がない場合は、 [現在の所有者メール]は、次の手順に従います。

1. からのメール転送の設定 [現在の所有者メール] 会社のメールサーバー設定を使用して新しいメールに送信します。
1. ここで、前の手順に進みます。

## 関連資料

[パスワードをリセット](https://helpx.adobe.com/manage-account/using/change-or-reset-password.html) （Creative Cloudユーザーガイド）を参照してください。
