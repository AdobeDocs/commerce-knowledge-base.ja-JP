---
title: Adobe CommerceおよびMagento Open Source 2.3.7-p2 のストック画像が表示されない
description: ここでは、ファイルシステムディレクトリ「pub/media」または「pub/media/catalog」にアップロードされたAdobeのストック画像が Media Gallery UI に表示されない問題の解決策について説明します。 これは、画像が許可されたメディアギャラリーディレクトリの外部にあるためです。 これらの画像をマーチャントに表示するには、ファイルシステム上の画像を削除し、許可されたメディアギャラリーディレクトリに再度アップロードする必要があります。
exl-id: 84488d87-095f-4739-858f-19a52d6e5822
feature: Categories, Orders
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# Adobe CommerceおよびMagento Open Source 2.3.7-p2 のストック画像が表示されない

ここでは、ファイルシステムディレクトリ `pub/media` または `pub/media/catalog` にアップロードされたAdobeのストック画像が Media Gallery UI に表示されない問題の解決策について説明します。 これは、画像が許可されたメディアギャラリーディレクトリの外部にあるためです。 これらの画像をマーチャントに表示するには、ファイルシステム上の画像を削除し、許可されたメディアギャラリーディレクトリに再度アップロードする必要があります。

## 影響を受ける製品とバージョン

* Adobe CommerceとMagento Open Source 2.3.7-p2


## 問題

マーチャントは、Adobe Stock画像をメディアギャラリーのストレージルートにアップロードできますが、これらの画像は UI に表示されず、アップロードされなかったかのように表示されます。 これは、Media Gallery UI では使用できませんが、画像がファイルシステムに既にアップロードされていることがシステムによって認識されるからです。 つまり、マーチャントが画像を `pub/media` または `pub/media/catalog` にアップロードすると、その画像がファイルシステム内で直接削除されるまで、その画像を使用できません。

<u> 再現手順 </u>

1. 有効な API キーでAdobe Stockを有効にします。
1. メディアギャラリー（**カタログ**/**カテゴリ**/**コンテンツ** セクションを開き、**ギャラリーから選択**）をクリックします。
1. **Adobe Stockを検索** をクリックします。
1. 画像を選択します。 「**プレビューを保存**」をクリックします。 画像を表示するには、Adobe Stockのグリッドをリセットする必要がある場合があります。

<u> 期待される結果 </u>:

画像が表示されます。

<u> 実際の結果 </u>:

次のエラーメッセージが表示されます。*画像が見つかりません。 この画像はメディア ギャラリーに見つかりません。*

## 原因：

Adobe Stockから Media Gallery のストレージルートに画像をアップロードできます。

## 解決策

Adobe Stock画像をアップロードする前に、Media Gallery ストレージルートのサブディレクトリ（「**ストレージルート**」 > 「**カタログ** を除く）を選択します。
アップロードしたAdobe Stock画像をAdobe Commerce ファイルシステムの `pub/media` フォルダーと `pub/media/catalog` フォルダーから削除し、許可されている Media Gallery ストレージルートのサブディレクトリ（**ストレージルート**/**カタログ** を除く）にアップロードします。

## 関連資料

* ユーザーガイドの [ メディアストレージ ](https://experienceleague.adobe.com/ja/docs/commerce-admin/content-design/wysiwyg/storage/media-storage)。
