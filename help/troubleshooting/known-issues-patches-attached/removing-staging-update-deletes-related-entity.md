---
title: ステージング更新を削除すると、関連エンティティが削除されます
description: この記事では、エンティティ（カテゴリ、CMS ページなど）に関連する既知のAdobe Commerce 2.2.3 問題に対するパッチを提供します 関連するスケジュールの更新が削除されると、それ自体が削除されます。
exl-id: 91138ac1-916e-4dd1-bad5-892524fdd9e1
feature: CMS, Cache, Categories, Staging
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# ステージング更新を削除すると、関連エンティティが削除されます

この記事では、エンティティ（カテゴリ、CMS ページなど）に関連する既知のAdobe Commerce 2.2.3 問題に対するパッチを提供します 関連するスケジュールの更新が削除されると、それ自体が削除されます。

>[!NOTE]
>
>この問題は、Adobe Commerce 2.2.6 で修正されました。

## 問題

開始日と終了日の間にあるアクティブなスケジュールの更新を削除すると、関連するエンティティ（カテゴリ、サブカテゴリ、CMS ページ）も削除されます。

<u>再現手順（カテゴリを使用）</u>:

1. Commerce Admin にログインします。
1. の下に新しいサブカテゴリを作成 **カタログ** > **カテゴリ**.
1. 開始時刻と終了時刻を指定して新しいステージング更新を作成します。
1. 更新が適用されるまで待ちます。つまり、開始時刻が来ます。
1. を使用して更新を削除します **表示/編集** リンク。

<u>期待される結果</u>:

更新は削除されますが、サブカテゴリは管理画面に残ります。

<u>実際の結果</u>:

更新とサブカテゴリが削除されます。

## 解決策

この記事で提供されているパッチを適用し、実行されているキャッシュをクリーンアップしてください

```bash
bin/magento
  cache:clean
```

## パッチ

パッチはこの記事に添付されています。 パッチをダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、対応するリンクをクリックします。

* [MDVA-11059\_EE\_2.2.3\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11059_EE_2.2.3_COMPOSER_v1.patch.zip)
* [MDVA-23505\_EE\_2.2.4\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-23505_EE_2.2.4_COMPOSER_v1.patch.zip)
* [MDVA-12158\_EE\_2.2.5\_COMPOSER\_v2.patch のダウンロード](assets/MDVA-12158_EE_2.2.5_COMPOSER_v2.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次の場合に作成されました。

* MDVA-11059\_EE\_2.2.3\_COMPOSER\_v1.patch は、Adobe Commerce（すべてのデプロイメント方式） 2.2.3 用に作成されました
* MDVA-23505\_EE\_2.2.4\_COMPOSER\_v1.patch は、Adobe Commerce（すべてのデプロイメント方式） 2.2.4 用に作成されました
* MDVA-12158\_EE\_2.2.5\_COMPOSER\_v2.patch は、Adobe Commerce（すべてのデプロイメント方式） 2.2.5 用に作成されました

MDVA-11059\_EE\_2.2.3\_COMPOSER\_v1.patch パッチも、次のAdobe Commerceのバージョンとエディションと互換性があります（ただし、問題が解決されない可能性があります）。

* Adobe Commerce オンプレミス 2.2.0-2.2.2
* クラウドインフラストラクチャー上のAdobe Commerce 2.2.0-2.2.3

MDVA-23505\_EE\_2.2.4\_COMPOSER\_v1.patch パッチも、次のAdobe Commerceのバージョンとエディションと互換性があります（ただし、問題が解決されない可能性があります）。

* Adobe Commerce オンプレミス 2.1.0 ～ 2.1.18、2.2.0 ～ 2.2.3
* クラウドインフラストラクチャー上のAdobe Commerce 2.1.0～2.1.18、2.2.0～2.2.3

MDVA-23505\_EE\_2.2.5\_COMPOSER\_v1.patch パッチも、次のAdobe Commerceのバージョンとエディションと互換性があります（ただし、問題が解決されない可能性があります）。

* クラウドインフラストラクチャー 2.2.5 上のAdobe Commerce

## パッチの適用方法

参照： [Adobe Commerceが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 説明を参照してください。

## 添付ファイル
