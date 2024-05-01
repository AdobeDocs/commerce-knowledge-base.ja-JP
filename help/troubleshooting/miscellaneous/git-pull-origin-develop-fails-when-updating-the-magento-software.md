---
title: Adobe Commerce ソフトウェアを更新すると、git プルオリジンの開発が失敗します
description: この記事では、「git プルオリジン開発」を実行しているときにAdobe Commerce ソフトウェアを更新できない場合の解決策を説明します。
exl-id: b133253e-c160-4f15-a9b0-8591e93a1e9b
feature: Upgrade
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Adobe Commerce ソフトウェアを更新すると、git プルオリジンの開発が失敗します

この記事では、の実行中にAdobe Commerce ソフトウェアを更新できない場合に対処する方法について説明します `git pull origin develop`.

## 詳細

Adobe Commerce ソフトウェアを更新する手順の 1 つは、次を実行してローカルリポジトリを更新することです。

```bash
$ git pull origin develop
```

次のエラーが表示される場合があります。

```terminal
error: Your local changes to the following files would be overwritten by merge:
<list of files>
```

上書きされる可能性があるファイルを見つけるには、メッセージを読むか、次のように入力します。

```bash
git status
```

次のセクションでは、提案される解決策について説明します。

### 提案される解決策

Adobe Commerce ファイルシステム内のファイルを意図的に変更したかどうかによって、解決策は異なります。 詳しくは、次のいずれかの節を参照してください。

#### ファイルを意図的に変更しました

競合は通常の方法で手動で解決します。 どうすればよいかわからない場合は、次を参照してください。 [GitHub ヘルプ](https://help.github.com/).

#### 意図的にファイルを変更していません

次のいずれかの操作を試します。

* ファイルを変更していないことがわかっていて、Adobe Commerce ファイルシステムの変更内容を削除したり上書きしたりしても構わない場合は、次のように入力します。

  </p>
    <pre><code class="language-bash">$ git reset --hard HEAD && git pull origin develop</code></pre>

  その後、Adobe Commerceの更新を中断した場所に進みます。

* GitHub 設定によって、今後これらのエラーを防ぐことができる可能性があります。 デフォルトでは、GitHub はオペレーティングシステムのデフォルトの行末文字を使用してコンテンツを保存します。 Linux を使用していて、別の共同作業者が Windows を使用して変更をコミットした場合、GitHub は、クローンまたはプル時に Windows の行末を Linux に変換します。 これにより、実際には変更が行われていないときに、ファイルに変更が加えられたように見えます。

  行末を無視するように GitHub を設定するには、Git クライアントで次のコマンドを入力します。

  </p>
    <pre><code class="language-bash">$ git config --system core.autocrlf false</code></pre>

  Windows を使用している場合は、次のように入力します。

  </p>
    <pre><code class="language-bash">$ git config --system core.eol LF</code></pre>

  >[!NOTE]
  >
  >Adobeは、特定の GitHub 設定を推奨または推奨しません。 上記は提案のみです。 詳しくは、次を参照してください [GitHub ヘルプ](https://help.github.com/).

  Adobe Commerceの更新を中断した場所に進みます。
