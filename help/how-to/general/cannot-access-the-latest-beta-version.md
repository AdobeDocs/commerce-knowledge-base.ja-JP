---
title: 最新のベータ版にアクセスできません
description: この記事では、Adobe Commerce用コードの最新ベータ版を利用しようとする際の問題の解決策について説明します。 ベータ版コードは、[Adobe Commerce ベータ版プログラム ] （https://github.com/magento/magento2/wiki/Magento-Beta-Program）に記載されているプロセスに従った公式Adobeパートナーのみが利用できます。
exl-id: a53c854e-38a8-4c8c-8586-9d99c576c835
source-git-commit: c1c2bd29e14f4cbfffb235801e95ec7cbb7c7a55
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# 最新のベータ版にアクセスできません

この記事では、Adobe Commerce用コードの最新ベータ版を利用しようとする際の問題の解決策について説明します。 ベータ版コードは、に記載されているプロセスに従った公式Adobeパートナーのみが利用できます。 [Adobe Commerce ベータ版プログラム](https://github.com/magento/magento2/wiki/Magento-Beta-Program).

## 問題

この記事では、早期アクセスコードへのアクセスに関する次の問題について説明します。

* Adobe Commerce ベータ版は、の下ではダウンロードできません **マイアカウント** > **Downloads** 日付： [magento.com](https://account.magento.com/customer/account/login).
* から早期アクセス用Adobe Commerce バージョンをダウンロードできない [magento.com](https://account.magento.com/customer/account/login) Composer を使用します。

## 原因：

問題の最も一般的な原因は次のとおりです。

* 間違った場所にあるアーリーアクセスコードを探しています。
* 間違った MageID を使用しています。
* 開発者には、正しい MageID からのアクセスキーが必要です。
* お使いのアカウントは、ベータ版プログラムには含まれていません。

## 解決策

### アーリーアクセスコードの場所

ベータ版のアクセス期間中、リリース パッケージは Composer を介してのみ [repo.magento.com](https://repo.magento.com/). この期間中、リリースパッケージは GitHub ポータルおよびAdobe Commerce ポータルでは利用できません。GA 日にこれらの場所に公開される予定です。 Composer の使用方法の詳細については、をクリックしてください。 [こちら](https://devdocs.magento.com/guides/v2.3/install-gde/composer.html).

### 使用する MageID

パートナーアカウントに関連付けられたプライマリ MageID を使用する必要があります。 ベータ版プログラムは、共有アクセス権を持つ連絡先にリンクされていません。 アーリーアクセスは、Composer または [repo.magento.com](https://repo.magento.com/) パートナーライセンスに関連付けられた MageID によって。

#### 自分の MageID がプライマリ ID かどうかを確認する方法

MageID がプライマリかどうかを確認するには、次の手順を実行します。

1. にログインします [magento.com](https://account.magento.com/customer/account/login) に移動します **マイ製品およびサービス** タブ。 「パートナー」サブセクションで、アクティブなパートナーライセンス情報が表示されているかどうかを確認します。
   * アクティブなパートナーライセンス情報が表示された場合、MageID はプライマリです。 終了日の値が将来の日付の場合、パートナーライセンスはアクティブになります。
   * アクティブなパートナーライセンス情報が表示されない場合、お使いの MageID には共有アクセスのみが付与されます。 プライマリ ID 所有者を確認するには、にアクセスしてください。 **自分と共有** ここで SHARENAME が指定されていることに注意してください。 クリック **アカウントの切り替え** SHARENAME でメモした値を選択します。 ようこそページに、プライマリ ID 所有者のメールが表示されます。
1. 何らかの理由でこの情報が見つからない場合： [magento.com](https://account.magento.com/customer/account/login)パートナー・マネージャにお問い合わせください。
1. 上記の方法で解決できない場合は、 [サポートに連絡する](/help/help-center-guide/help-center/magento-help-center-user-guide.md#merchant-not-displayed).

#### 開発者は、キーに対する適切なアクセス権を持っていません

メインの MageID オーナーで、チームの開発者にアクセス権を付与する必要がある場合は、次の手順に従います。

1. プライマリ MageID 所有者をにログインさせる [account.magento.com](https://account.magento.com/customer/account/login).
1. 「」を選択します **Marketplace** tab キーを押してクリックします **アクセスキー**.
1. を選択 **新しいアクセスキーの作成** という名前を付けます。
1. 開発者にキーを送信します。

### アーリーアクセスプログラムに含まれていません

ベータ版アクセスプログラムは、アドビのソリューションパートナーおよびテクニカルパートナーのみが使用できるので、アドビの実稼動前のコードを評価できます。 ベータ版アクセスプログラムに含めるには、準備完了でベータ版 NDA に署名したアクティブなAdobeパートナーアカウントが必要です [こちら](https://github.com/magento/magento2/wiki/Magento-Beta-Program). これらの条件を満たしていて、ベータ版コードにアクセスできない場合は、にお問い合わせください [commercebeta@adobe.com](mailto:commercebeta@adobe.com).
