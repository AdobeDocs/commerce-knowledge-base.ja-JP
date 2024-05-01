---
title: Adobeが提供する composer パッチの適用方法
description: この文書では、Adobe Commerce オンプレミス、Adobe Commerce on cloud infrastructure、およびMagento Open Sourceに composer パッチを適用する方法について説明します。
exl-id: a9301ad8-1d4b-49f5-b679-758624928219
feature: Cache
source-git-commit: 83b21845cd306336e1cb193a9541478c8a38eea8
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Adobeが提供する composer パッチの適用方法

この文書では、Adobe Commerce オンプレミス、Adobe Commerce on cloud infrastructure、およびMagento Open Sourceに composer パッチを適用する方法について説明します。

>[!WARNING]
>
>実稼動環境に適用する前に、ステージング環境または統合環境でパッチを適用してテストすることを強くお勧めします。 また、操作を行う前に、最新のバックアップを作成することをお勧めします。

## クラウドインフラストラクチャー上のAdobe Commerceに composer パッチを適用する方法 {#cloud}

1. というディレクトリがない場合 `m2-hotfixes` プロジェクトルートに作成してください。
1. をコピーします `%patch_name%.composer.patch` 個のファイルを `m2-hotfixes` ディレクトリ。
1. コードの変更を追加、コミット、プッシュします。

   ```git
   git add -A
   ```

   ```git
   git commit -m "Apply %patch_name%.composer.patch patch"
   ```

   ```git
   git push origin
   ```

クラウドプロジェクトにパッチを適用する方法については、を参照してください。 [パッチの適用](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

### Adobe Commerceのオンプレミス環境およびMagento Open Sourceに composer パッチを適用する方法 {#commerce}

1. Adobe CommerceのオンプレミスまたはMagento Open Sourceのルートディレクトリにパッチをアップロードします。
1. 次の SSH コマンドを実行します。

   ```bash
   patch -p1 < %patch_name%.composer.patch
   ```

   （上記のコマンドが機能しない場合は、を使用してみてください。 `-p2` の代わりに `-p1` ）

1. 変更を反映するには、の管理画面でキャッシュを更新します。 **システム** > **キャッシュ管理**.
