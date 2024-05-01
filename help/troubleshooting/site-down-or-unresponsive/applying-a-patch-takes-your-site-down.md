---
title: パッチを適用すると、サイトが停止します
description: この記事では、適用したばかりのパッチがサイトをダウンさせる問題について説明します。 これを解決するには、パッチを削除します。
exl-id: dc765bcd-0761-4efd-a345-46a908d61272
feature: Cache
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# パッチを適用すると、サイトが停止します

この記事では、適用したばかりのパッチがサイトをダウンさせる問題について説明します。 これを解決するには、パッチを削除します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）、すべてのサポートされているバージョン
* Magento Open Source、すべてのバージョン

## 問題

パッチを適用すると、サイトが停止します。

## 原因：

この問題は、Web サイトに適用したパッチ、カスタマイズ、以前に適用した他のパッチ、またはその他のエラーとのバージョンの非互換性が原因で発生する場合があります。

## 解決策

パッチを取り外します。 パッチの削除方法は、Adobe Commerce on cloud infrastructure の場合と、Adobe Commerce オンプレミスおよびMagento Open Sourceの場合で異なります。

### Magento Open Source、すべての 1.X バージョン

Magento Open Source 1.X の場合、

* 次の SSH コマンドを実行します。 `h SUPEE_patch --revert `

### Adobe Commerce オンプレミス、Magento Open Source、すべての 2.x バージョン

Adobe Commerce オンプレミスおよびMagento Open Source 2.x バージョンの場合、

1. 次の SSH コマンドを実行します。

   ```
   patch -p1 -R %patch_name%.composer.patch
   ```

   （上記のコマンドが機能しない場合は、を使用してみてください。 `-p2` の代わりに `-p1`）

1. 変更を反映するには、の管理画面でキャッシュを更新します。 **システム** > **キャッシュ管理**.

### クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

クラウドインフラストラクチャー上のAdobe Commerceの場合、すべてのバージョン、

1. を削除 `%patch_name%.composer.patch` 個のファイル （から） `m2-hotfixes` ディレクトリ。
1. コードの変更をコミットしプッシュします。

   ```
   git commit -m "Remove %patch_name%.composer.patch patch" && git push origin
   ```

## 関連資料

* [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。
