---
source-git-commit: c587986edc925c49bf95ab935888b59f265371af
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---
# KB 形式ガイド

## Markdown での作成者

通常、[Adobe Experience League Markdown 構文スタイルガイド ](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/markdown/syntax-style-guide.html?lang=ja) を使用しますが、いくつかの違いがあり、例外があります。 また、場合によっては、特定のHTMLタグが必要です。

リポジトリーで最も一般的に使用される Markdown フォーマットの例を以下に示します。

## 基本的な書式設定

テキストを太字にするには、次の 2 つのアスタリスクで囲みます。

`This will be **bold** text`

テキストを斜体として書式設定するには、アスタリスクを 1 つ使用します。

`This text will be *italics*`

テキストを下線付きとして書式設定するには、`<ins>` のタグを使用します。

`<ins>This text will be underlined</ins>`

改行を追加するには、`<br>` のHTMLタグを使用します。


## ヘッダー

H2 から H5 のヘッダーには、次の書式を使用します。 記事のタイトルが H1 と見なされるので、H1 は使用されません。

`## Header 2 `

`### Header 3 `

`#### Header 4`

`##### Header 5`

## コードをインラインおよびブロック化

ハイライトするコード要素を囲むために、バッククォートを 1 つ使用します。

これはテキストの段落内の\&#39;インラインコード\&#39;です。

### コードブロック

コードブロックを挿入するには、コードブロックを 3 つのバッククォートで囲み、3 つのバッククォートを開いた後で言語を指定します。

\&#39;\&#39;\&#39; sql

TABLE_NAME を `Table` として選択します。
ROUND （（DATA_LENGTH + INDEX_LENGTH） / 1024 / 1024） AS `Size (MB)`
FROM information_schema.TABLES
TABLE_SCHEMA = &quot;%project_id%&quot;
（DATA_LENGTH + INDEX_LENGTH）降順；

\&#39;\&#39;\&#39;

これは、次のようにレンダリングされます。

```sql
SELECT TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024) AS `Size (MB)`
FROM information_schema.TABLES
WHERE TABLE_SCHEMA = "%project_id%"
ORDER BY (DATA_LENGTH + INDEX_LENGTH) DESC;
```

リンティングルールに従って、コードブロックの言語を常に指定する必要があります。

サポートされる言語の一覧は、https://github.com/github/linguist/blob/master/lib/linguist/languages.ymlを参照してください。

Markdown で特定の言語がハイライト表示されない場合（つまり言語がサポートされていない場合）、https://support.magento.com/hc/en-us/に公開したときに少なくともハイライト表示されるようにするには、次のHTMLを使用します。

```html
<pre><code class="language-%language-code%"
your code here
</pre></code>
```

ここで、``%language-code%`` は [Prism.js でサポートされる言語 ](https://prismjs.com/#supported-languages) で定義されるコードです。

## リスト

リストは、常に空白行でコンテンツの残りの部分から分離します。 リストの先頭および後には空白行を付ける必要があります。

順序付きリストには次の書式を使用します。

```markdown
1. First numbered list item.
1. Second numbered list item.
...
1. Last numbered list item.
```

順序なし箇条書きリストを作成するには、行を*、+または – で始めます。 ただし、1 つの方法を選択し、記事全体を通して一貫して使用します。

例：

```markdown
* Unordered list item.
* Unordered list item.
---
* Last unordered list item.
```

リスト項目間にコンテンツを追加するには、行の先頭に 4 つのスペースを追加します。

```markdown
* List item.
* List item.
    Here's some content between list items.
* Here we continue the list
```

この方法でリストを埋め込むこともできます。

## リンク

外部リンクは簡単です。

```markdown
[Adobe](https://www.adobe.com)
```

### 添付ファイルへのリンク

あらゆる種類の添付ファイルは、.png、.jpg および.jpeg 形式である必要があります。 セキュリティ上の目的で、3 つの形式のいずれかの添付ファイルのみを受け入れます。

画像を挿入するには、画像を記事と同じセクションフォルダーの *assets* サブフォルダーに配置し、次の構文を使用して画像を記事に挿入します。

```markdown
![alt text](assets/image.png)
```

画像のサイズをカスタマイズする場合は、次のHTMLタグを使用する必要があります。

```html
<img src = "assets/image.png" alt = "your alt text" width="custom width, ex: 250px">
```

```markdown
[asset_title](assets/%file_name%).
```

### 記事の特定のセクションへのリンク

記事内のセクションを参照する必要がある場合は、別のアンカーを作成する必要はありません。 すべての H2～H6 見出しの公開時に自動的に生成されます。 アンカーは、すべての単語を小文字にし、単語を区切るために「–」を使用することによって、ヘッダーから生成されます。

例：

```markdown
## This is header
```

このヘッダーへのリンクは次のとおりです。

```markdown
[this is link to the anchor in the same article](#this-is-header)
```

header 以外の要素を参照する必要がある場合は、HTMLを使用して、追加する要素を定義し、[id 属性 ](https://www.w3schools.com/html/html_id.asp) を使用します。 その後、Markdown またはHTMLを使用して、この ID を参照できます。

### 他の記事への相対リンクとリンク

サポートナレッジベースの記事を参照するために相対リンクを使用しないでください。 記事が [Adobe Commerce ヘルプセンター ](https://support.magento.com/hc/en-us) で公開されると、これらのリンクは機能しません。
[Adobe Commerce ヘルプ センター ](https://support.magento.com/hc/en-us) のハイパーリンクをすべて使用してください。


## テーブル

テーブルには [HTML形式を使用 ](https://www.w3schools.com/html/html_tables.asp) ます。


## 警告および情報ブロック

成功メモ ブロック：

```
>![success]
>
>This is a success note
```

警告ブロック：

```
>![warning]
>
>This is a warning
```

情報メモ ブロック：

```
>![info]
>
>This is a block with additional info
```
