---
title: Adobeが提供する composer パッチの適用方法
description: この文書では、Adobe Commerce オンプレミス、Adobe Commerce on cloud infrastructure、およびMagento Open Sourceに composer パッチを適用する方法について説明します。
exl-id: a9301ad8-1d4b-49f5-b679-758624928219
feature: Cache
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

1. プロジェクトルートに `m2-hotfixes` という名前のディレクトリがない場合は作成してください。
1. `%patch_name%.composer.patch` ファイルを `m2-hotfixes` ディレクトリにコピーします。
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

クラウドプロジェクトにパッチを適用する方法について詳しくは、開発者向けドキュメントの [ パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches) を参照してください。

### Adobe Commerceのオンプレミス環境およびMagento Open Sourceに composer パッチを適用する方法 {#commerce}

1. Adobe CommerceのオンプレミスまたはMagento Open Sourceのルートディレクトリにパッチをアップロードします。
1. 次の SSH コマンドを実行します。

   ```bash
   patch -p1 < %patch_name%.composer.patch
   ```

   （上記のコマンドが機能しない場合は、`-p1` の代わりに `-p2` を使用してみてください）

1. 変更を反映するには、管理画面の **システム**/**キャッシュ管理** でキャッシュを更新します。
