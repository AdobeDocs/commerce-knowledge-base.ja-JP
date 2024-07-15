---
title: VAT 番号を検証できません – クラウドインフラストラクチャー上のAdobe Commerce
description: この記事では、VAT 番号の検証中にエラーが発生した問題に対するパッチを提供します。
exl-id: 9868e888-bad8-4823-acab-4b3804933cb0
feature: Cloud, Customer Service, Paas
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# VAT 番号を検証できません – クラウドインフラストラクチャー上のAdobe Commerce

この記事では、VAT 番号の検証中にエラーが発生した問題に対するパッチを提供します。

## 影響を受ける製品とバージョン

既にリリースされている p1 および p2 バージョンを含め、2.3.6 までのすべてのAdobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure バージョン（2.3.5-p1 を含む）が影響を受けました。 これには以下が含まれます。

* 2.3.5-p1
* 2.3.5
* 2.3.4 - 2.3.4-p2
* 2.3.3 - 2.3.3-p1
* 2.3.2 -2.3.2-p2
* 2.0.0 - 2.3.1

## 問題

<u> 再現手順：</u>

1. **ストア**/**設定**/**顧客**/**顧客設定**/**新しいアカウントオプションを作成** に移動し、**自動割り当てを有効にする** を **顧客グループ** に設定して *はい* にします。
1. **一般**/**店舗情報**/に移動し、有効な国と VAT 番号を設定します。
1. **VAT 番号の検証** をクリックします。

<u> 期待される結果：</u>

検証に成功しました。

<u> 実際の結果：</u>

「*VAT 番号の検証中にエラーが発生しました*」というエラーが表示されます

## 解決策

この記事で提供されている [ パッチ ](assets/MDVA-27623_EE_2.3.2-p2_COMPOSER_v1.patch.zip) を適用します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-27623\_EE\_2.3.2-p2\_COMPOSER\_v1.patch](assets/MDVA-27623_EE_2.3.2-p2_COMPOSER_v1.patch.zip)

## パッチの適用方法

手順については、[Adobeが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 添付ファイル
