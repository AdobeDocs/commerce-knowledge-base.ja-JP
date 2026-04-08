---
title: 現在のAdobe アカウントのメールアドレスを変更する
description: Adobe アカウントに登録されている現在の電子メールアドレスを、Adobe アカウントまたはMagento アカウントに登録されていない新しいアドレスに変更する方法について説明します。
exl-id: ca549d38-0d62-4206-9727-0ed85b733dc3
feature: Communications
source-git-commit: 2fc3353c7563cff6fb82236d40a91306523a579e
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# 現在のAdobe アカウントのメールアドレスを変更する

この記事では、[Adobe アカウント &#x200B;](https://account.adobe.com/)に登録されている現在の電子メールアドレスを、[Adobe アカウント &#x200B;](https://account.adobe.com/)または[Magento アカウント &#x200B;](https://account.magento.com/)に現在登録されていない新しいアドレスに変更する方法について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法とバージョン）

## 前提条件

新しいメールアドレスの所有者は、現在のメールアドレスにアクセスできる必要があります。

現在のメールアドレスにアクセスできない場合は、会社のメールサーバー設定を使用して、現在の所有者のメールから新しいメールへのメール転送を設定します。

## メールアドレスの変更手順

電子メールアドレスを変更するには、次の手順に従います。

1. 古いメールアドレスで使用したパスワードをリセットします。 Adobe helpxの[&#x200B; パスワードを忘れた場合のリセット &#x200B;](https://helpx.adobe.com/manage-account/using/change-or-reset-password.html)の手順に従います。
1. パスワードリセットリンクは、現在の所有者のメールボックスに指示とともに送信されます。
1. [Adobe アカウントページ &#x200B;](https://account.adobe.com)に移動して、新しい電子メールでログインし、パスワードを設定します。

## 重要：クラウドアカウントのユーザー名が自動的に更新されない

クラウドインフラストラクチャでAdobe Commerceを使用している場合、Adobe アカウントまたはMAGE IDのメールアドレスを変更しても、[&#x200B; クラウドアカウント &#x200B;](https://accounts.magento.cloud)に表示されているユーザー名は自動的に更新されません。

この記事の手順を完了して、Adobe アカウントのメールアドレスを変更します。

1. [https://accounts.magento.cloud](https://accounts.magento.cloud)でCloud アカウントにログインします。
1. [&#x200B; サポートナレッジベースのクラウドアカウントプロファイルの更新方法](/help/how-to/general/how-to-update-the-cloud-account-profile.md)の手順に従って、クラウドアカウントプロファイル（ユーザー名）を手動で更新します。

これにより、Cloud アカウントのユーザー名が更新されたAdobeまたはMAGE IDの電子メールと一致し、クラウドプロジェクトにアクセスしたり、システム通知を受け取ったりする際の混乱を回避できます。

## メールの変更後にマーケットプレイスとサポートのアクセスを確認する

MAGE IDのメールアドレスを変更した後、Adobe Commerce Marketplaceとサポートが新しいメールを正しく認識するように、次の手順を実行する必要があります。

### Commerce Marketplaceの電子メールを確認

1. [https://commercemarketplace.com/customer/account](https://commercemarketplace.com/customer/account)にログインし、アカウントの電子メールが新しいアドレスに更新されたことを確認します。
1. 電子メールが更新されていない場合は、Commerce Marketplace アカウントの電子メールの修正を依頼する[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/en/support#home)を送信します。

### サポートに連絡して、社内アカウントの更新を最終調整してもらう

1. [&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/en/support#home)を送信して、必要な内部更新を完了するよう求めます（例えば、古いAdobe IDと新しいMAGE IDのリンクを更新します）。
1. 以前のセクションでCommerce Marketplaceの電子メールが更新されなかったため、サポートチケットを既に開いている場合は、同じチケットを使用して、これらの内部更新をリクエストできます。
