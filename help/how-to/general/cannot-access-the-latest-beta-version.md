---
title: 最新バージョンのBetaにアクセスできません
description: この記事では、最新バージョンのBeta code for Adobe Commerceを利用しようとする際の問題の解決策について説明します。 Beta コードは、[Adobe Commerce Beta プログラム ] （https://github.com/magento/magento2/wiki/Magento-Beta-Program）に記載されているプロセスに従った、公式のAdobeパートナーのみが利用できます。
exl-id: a53c854e-38a8-4c8c-8586-9d99c576c835
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# 最新バージョンのBetaにアクセスできません

この記事では、最新バージョンのBeta code for Adobe Commerceを利用しようとする際の問題の解決策について説明します。 Beta コードは、[Adobe Commerce Beta プログラム &#x200B;](https://github.com/magento/magento2/wiki/Magento-Beta-Program) に記載されているプロセスに従った、公式のAdobeパートナーのみが利用できます。

## 問題

この記事では、早期アクセスコードへのアクセスに関する次の問題について説明します。

* Adobe Commerce Betaのバージョンは、[magento.com](https://account.magento.com/customer/account/login) の **マイアカウント**/**ダウンロード** ではダウンロードできません。
* Composer を使用して [magento.com](https://account.magento.com/customer/account/login) からアーリーアクセス Adobe Commerce バージョンをダウンロードできない。

## 原因：

問題の最も一般的な原因は次のとおりです。

* 間違った場所にあるアーリーアクセスコードを探しています。
* 間違った MageID を使用しています。
* 開発者には、正しい MageID からのアクセスキーが必要です。
* アカウントは、Beta プログラムには含まれていません。

## 解決策

### アーリーアクセスコードの場所

ベータ版のアクセス期間中、リリースパッケージは [repo.magento.com](https://repo.magento.com/) の Composer からのみ入手できます。 この期間中、リリースパッケージは GitHub ポータルおよびAdobe Commerce ポータルでは利用できません。GA 日にこれらの場所に公開される予定です。 Composer の使用方法の詳細については、[&#x200B; こちら &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/composer) をクリックしてください。

### 使用する MageID

パートナーアカウントに関連付けられたプライマリ MageID を使用する必要があります。 Beta プログラムは、共有アクセス権を持つ連絡先にリンクされていません。 アーリーアクセスは、Composer または [repo.magento.com](https://repo.magento.com/) 経由でのみ、パートナーライセンスに関連付けられた MageID でアクセスできます。

#### 自分の MageID がプライマリ ID かどうかを確認する方法

MageID がプライマリかどうかを確認するには、次の手順を実行します。

1. [magento.com](https://account.magento.com/customer/account/login) にログインし、「製品とサービス **タブに移動** ます。 「パートナー」サブセクションで、アクティブなパートナーライセンス情報が表示されているかどうかを確認します。
   * アクティブなパートナーライセンス情報が表示された場合、MageID はプライマリです。 終了日の値が将来の日付の場合、パートナーライセンスはアクティブになります。
   * アクティブなパートナーライセンス情報が表示されない場合、お使いの MageID には共有アクセスのみが付与されます。 プライマリ ID 所有者を確認するには、**自分と共有** に移動します。ここで指定されている SHARENAME に注意してください。 **アカウントの切り替え** をクリックし、SHARENAME でメモした値を選択します。 ようこそページに、プライマリ ID 所有者のメールが表示されます。
1. 何らかの理由でこの情報が [magento.com](https://account.magento.com/customer/account/login) で見つからない場合は、パートナーマネージャーにお問い合わせください。
1. 上記の方法で解決できない場合は、[&#x200B; サポートにお問い合わせください &#x200B;](/help/help-center-guide/help-center/magento-help-center-user-guide.md#merchant-not-displayed)。

#### 開発者は、キーに対する適切なアクセス権を持っていません

メインの MageID オーナーで、チームの開発者にアクセス権を付与する必要がある場合は、次の手順に従います。

1. プライマリ MageID 所有者を [account.magento.com](https://account.magento.com/customer/account/login) にログインしてもらいます。
1. 「**Marketplace**」タブを選択し、「**アクセスキー**」をクリックします。
1. 「**新しいアクセスキーを作成**」を選択し、名前を付けます。
1. 開発者にキーを送信します。

### アーリーアクセスプログラムに含まれていません

アドビのBeta アクセスプログラムは、アドビのソリューションパートナーおよびテクニカルパートナーのみが利用できるので、アドビの実稼動前のコードを評価できます。 Beta アクセスプログラムに含めるには、正常に機能し、Beta NDA [&#x200B; こちら &#x200B;](https://github.com/magento/magento2/wiki/Magento-Beta-Program) に署名したアクティブなAdobeパートナーアカウントが必要です。 これらの条件を満たしていて、ベータ版コードにアクセスできない場合は、[commercebeta@adobe.com](mailto:commercebeta@adobe.com) にお問い合わせください。
